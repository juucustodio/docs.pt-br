---
title: Credenciais do canal-gRPC para desenvolvedores do WCF
description: Como implementar e usar as credenciais de canal do gRPC no ASP.NET Core 3,0.
ms.date: 12/15/2020
ms.openlocfilehash: 3663bbf061156db957241e2a32dbb9c64562ade2
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938631"
---
# <a name="channel-credentials"></a>Credenciais de canal

Como o nome indica, as credenciais de canal são anexadas ao canal gRPC subjacente. A forma padrão de credenciais de canal usa a autenticação de certificado do cliente. Nesse processo, o cliente fornece um certificado TLS quando está fazendo a conexão e, em seguida, o servidor verifica esse certificado antes de permitir que qualquer chamada seja feita.

Você pode combinar credenciais de canal com credenciais de chamada para fornecer segurança abrangente para um serviço gRPC. As credenciais do canal provam que o aplicativo cliente tem permissão para acessar o serviço e as credenciais de chamada fornecem informações sobre a pessoa que está usando o aplicativo cliente.

A autenticação de certificado de cliente funciona para gRPC da mesma maneira que funciona para ASP.NET Core. Para obter mais informações, consulte [Configurar a autenticação de certificado no ASP.NET Core](/aspnet/core/security/authentication/certauth).

Para fins de desenvolvimento, você pode usar um certificado autoassinado, mas para produção, você deve usar um certificado HTTPS adequado assinado por uma autoridade confiável.

## <a name="add-certificate-authentication-to-the-server"></a>Adicionar autenticação de certificado ao servidor

Configure a autenticação de certificado no nível do host (por exemplo, no servidor Kestrel) e no pipeline ASP.NET Core.

### <a name="configure-certificate-validation-on-kestrel"></a>Configurar a validação de certificado no Kestrel

Você pode configurar Kestrel (o servidor HTTP ASP.NET Core) para exigir um certificado de cliente e, opcionalmente, realizar alguma validação do certificado fornecido, antes de aceitar conexões de entrada. Você especifica essa configuração no `CreateWebHostBuilder` método da `Program` classe, em vez de em `Startup` .

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureWebHostDefaults(webBuilder =>
        {
            var serverCert = ObtainServerCertificate();
            webBuilder.UseStartup<Startup>()
                .ConfigureKestrel(kestrelServerOptions => {
                    kestrelServerOptions.ConfigureHttpsDefaults(opt =>
                    {
                        opt.ClientCertificateMode = ClientCertificateMode.RequireCertificate;

                        // Verify that client certificate was issued by same CA as server certificate
                        opt.ClientCertificateValidation = (certificate, chain, errors) =>
                            certificate.Issuer == serverCert.Issuer;
                    });
                });
        });

```

A `ClientCertificateMode.RequireCertificate` configuração faz com que o Kestrel rejeite imediatamente qualquer solicitação de conexão que não forneça um certificado de cliente, mas essa configuração por si só não validará um certificado fornecido. Adicione o `ClientCertificateValidation` retorno de chamada para permitir que o Kestrel valide o certificado do cliente no ponto em que a conexão é feita, antes que o pipeline de ASP.NET Core seja envolvido. (Nesse caso, o retorno de chamada garante que ele foi emitido pela mesma *autoridade de certificação* que o certificado do servidor.)

### <a name="add-aspnet-core-certificate-authentication"></a>Adicionar ASP.NET Core autenticação de certificado

O pacote NuGet [Microsoft. AspNetCore. Authentication. Certificate](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Certificate) fornece autenticação de certificado.

Adicione o serviço de autenticação de certificado no `ConfigureServices` método e adicione autenticação e autorização ao pipeline de ASP.NET Core no `Configure` método.

```csharp
public class Startup
{
    private readonly bool _isDevelopment;

    public Startup(IWebHostEnvironment env)
    {
        _isDevelopment = env.IsDevelopment();
    }

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(CertificateAuthenticationDefaults.AuthenticationScheme)
            .AddCertificate(options =>
            {
                if (_isDevelopment)
                {
                    // DO NOT DO THIS IN PRODUCTION!
                    options.RevocationMode = X509RevocationMode.NoCheck;
                }
            });
        services.AddAuthorization();
        services.AddGrpc();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        app.UseRouting();

        app.UseAuthentication();
        app.UseAuthorization();

        app.UseEndpoints(endpoints => { endpoints.MapGrpcService<GreeterService>(); });
    }
}
```

## <a name="provide-channel-credentials-in-the-client-application"></a>Fornecer credenciais de canal no aplicativo cliente

Com o `Grpc.Net.Client` pacote, você configura certificados em uma <xref:System.Net.Http.HttpClient> instância do que é fornecida para o `GrpcChannel` usado para a conexão.

```csharp
class Program
{
    static async Task Main(string[] args)
    {
        // Assume path to a client .pfx file and password are passed from command line
        // On Windows this would probably be a reference to the Certificate Store
        var cert = new X509Certificate2(args[0], args[1]);

        var handler = new HttpClientHandler();
        handler.ClientCertificates.Add(cert);
        var httpClient = new HttpClient(handler);

        var channel = GrpcChannel.ForAddress("https://localhost:5001/", new GrpcChannelOptions
        {
            HttpClient = httpClient
        });

        var grpc = new Greeter.GreeterClient(channel);
        var response = await grpc.SayHelloAsync(new HelloRequest { Name = "Bob" });
        System.Console.WriteLine(response.Message);
    }
}
```

## <a name="combine-channelcredentials-and-callcredentials"></a>Combinar ChannelCredentials e CallCredentials

Você pode configurar o servidor para usar a autenticação de certificado e de token. Para fazer isso, aplique as alterações de certificado ao servidor Kestrel e use o middleware portador JWT no ASP.NET Core.

Para fornecer `ChannelCredentials` e `CallCredentials` no cliente, use o `ChannelCredentials.Create` método para aplicar as credenciais de chamada. Você ainda precisa aplicar a autenticação de certificado usando a <xref:System.Net.Http.HttpClient> instância do. Se você passar quaisquer argumentos para o `SslCredentials` Construtor, o código do cliente interno lançará uma exceção. O `SslCredentials` parâmetro só é incluído no `Grpc.Net.Client` método do pacote `Create` para manter a compatibilidade com o `Grpc.Core` pacote.

```csharp
var handler = new HttpClientHandler();
handler.ClientCertificates.Add(cert);

var httpClient = new HttpClient(handler);

var callCredentials = CallCredentials.FromInterceptor(((context, metadata) =>
    {
        metadata.Add("Authorization", $"Bearer {_token}");
    }));

var channelCredentials = ChannelCredentials.Create(new SslCredentials(), callCredentials);

var channel = GrpcChannel.ForAddress("https://localhost:5001/", new GrpcChannelOptions
{
    HttpClient = httpClient,
    Credentials = channelCredentials
});

var grpc = new Portfolios.PortfoliosClient(channel);
```

> [!TIP]
> Você pode usar o `ChannelCredentials.Create` método para um cliente sem autenticação de certificado. Essa é uma maneira útil de passar credenciais de token com cada chamada feita no canal.

Uma versão do [aplicativo de exemplo FullStockTicker gRPC com autenticação de certificado adicionada](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/FullStockTickerSample/grpc/FullStockTickerAuth/FullStockTicker) está no github.

>[!div class="step-by-step"]
>[Anterior](call-credentials.md) 
> [Avançar](encryption.md)
