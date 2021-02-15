---
title: Credenciais de chamada-gRPC para desenvolvedores do WCF
description: Como implementar e usar as credenciais de chamada do gRPC no ASP.NET Core 3,0.
ms.date: 12/15/2020
ms.openlocfilehash: 66394c75929bf068f83d631e022b467386e59ec5
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938436"
---
# <a name="call-credentials"></a>Credenciais de chamada

As credenciais de chamada são todas baseadas em um token passado em metadados com cada solicitação.

## <a name="ws-federation"></a>O certificado do provedor de identidade do Web Services Federation

ASP.NET Core dá suporte a WS-Federation usando o pacote NuGet [WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) . WS-Federation é a alternativa mais próxima disponível para a autenticação do Windows, que não tem suporte por HTTP/2. Os usuários são autenticados usando Serviços de Federação do Active Directory (AD FS) (AD FS), que fornece um token que pode ser usado para autenticar com ASP.NET Core.

Para obter mais informações sobre como começar a usar esse método de autenticação, consulte [autenticar usuários com WS-Federation no ASP.NET Core](/aspnet/core/security/authentication/ws-federation).

## <a name="jwt-bearer-tokens"></a>Tokens de portador JWT

O padrão JWT ( [token Web JSON](https://jwt.io) ) fornece uma maneira de codificar informações sobre um usuário e suas declarações em uma cadeia de caracteres codificada. Ele também fornece uma maneira de assinar esse token, para que o consumidor possa verificar a integridade do token usando criptografia de chave pública. Você pode usar vários serviços, como IdentityServer4, para autenticar usuários e gerar tokens de OpenID Connect (OIDC) para usar com APIs de gRPC e HTTP.

ASP.NET Core 5,0 pode manipular JWTs usando o pacote de portador JWT. A configuração é exatamente a mesma para um aplicativo gRPC como se trata de um aplicativo MVC ASP.NET Core. Aqui, nos concentraremos nos tokens de portador JWT, pois eles são mais fáceis de desenvolver com o WS-Federation.

## <a name="add-authentication-and-authorization-to-the-server"></a>Adicionar autenticação e autorização ao servidor

O pacote de portador JWT não está incluído no ASP.NET Core 5,0 por padrão. Instale o pacote NuGet [Microsoft. AspNetCore. Authentication. JwtBearer](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.JwtBearer) em seu aplicativo.

Adicione o serviço de autenticação na classe de inicialização e configure o manipulador de portador JWT:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddGrpc();

    var signingKey = ObtainSigningKeySomehow();

    services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddJwtBearer(options =>
        {
            options.TokenValidationParameters =
                new TokenValidationParameters
                {
                    ValidateAudience = false,
                    ValidateIssuer = false,
                    ValidateActor = false,
                    ValidateLifetime = true,
                    IssuerSigningKey = signingKey
                };
        });

}
```

A `IssuerSigningKey` propriedade requer uma implementação de `Microsoft.IdentityModels.Tokens.SecurityKey` com os dados criptográficos necessários para validar os tokens assinados. Armazene esse token com segurança em um *servidor de segredos*, como Azure Key Vault.

Em seguida, adicione o serviço de autorização, que controla o acesso ao sistema:

```csharp
    services.AddAuthorization(options =>
    {
        options.AddPolicy(JwtBearerDefaults.AuthenticationScheme, policy =>
        {
            policy.AddAuthenticationSchemes(JwtBearerDefaults.AuthenticationScheme);
            policy.RequireClaim(ClaimTypes.Name);
        });
    });

```

> [!TIP]
> Autenticação e autorização são duas etapas separadas. Você usa a autenticação para determinar a identidade do usuário. Você pode usar a autorização para decidir se esse usuário tem permissão para acessar várias partes do sistema.

Agora, adicione o middleware de autenticação e autorização ao pipeline ASP.NET Core no `Configure` método:

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseRouting();

    // Authenticate, then Authorize
    app.UseAuthentication();
    app.UseAuthorization();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapGrpcService<PortfolioService>();
    });
}
```

Por fim, aplique o `[Authorize]` atributo a qualquer serviço ou método a ser protegido e use a `User` Propriedade do subjacente `HttpContext` para verificar as permissões.

```csharp
[Authorize]
public override async Task<GetResponse> Get(GetRequest request, ServerCallContext context)
{
    if (!TryValidateUser(request.TraderId, context.GetHttpContext().User))
    {
        throw new RpcException(new Status(StatusCode.PermissionDenied, "Denied."));
    }

    var portfolio = await _repository.GetAsync(traderId, request.PortfolioId);

    return new GetResponse
    {
        Portfolio = Portfolio.FromRepositoryModel(portfolio)
    };
}
```

## <a name="provide-call-credentials-in-the-client-application"></a>Fornecer credenciais de chamada no aplicativo cliente

Depois de obter um token JWT de um servidor de identidade, você pode usá-lo para autenticar chamadas gRPC do cliente adicionando-o como um cabeçalho de metadados na chamada, da seguinte maneira:

```csharp
public async Task ShowPortfolioAsync(int portfolioId)
{
    var headers = new Grpc.Core.Metadata
    {
        { "Authorization", $"Bearer {_userToken}" }
    };
    var request = new GetRequest
    {
        TraderId = _userId,
        PortfolioId = portfolioId
    };
    var response = await _portfoliosClient.GetAsync(request, headers);

    // Display portfolio
}
```

Agora você protegeu seu serviço gRPC usando tokens de portador JWT como credenciais de chamada. Uma versão do [aplicativo gRPC de exemplo de portfólios com autenticação e autorização adicionada](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/PortfoliosSample/grpc/TraderSysAuth) está no github.

>[!div class="step-by-step"]
>[Anterior](security.md) 
> [Avançar](channel-credentials.md)
