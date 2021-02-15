---
title: Host Genérico .NET
author: IEvangelist
description: Saiba mais sobre o host genérico do .NET, que é responsável pela inicialização do aplicativo e pelo gerenciamento do tempo de vida.
ms.author: dapine
ms.date: 12/18/2020
ms.openlocfilehash: bf6d5ad624bbed46994633abace0af64712757f3
ms.sourcegitcommit: 3d6d6595a03915f617349781f455f838a44b0f44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97700730"
---
# <a name="net-generic-host"></a>Host Genérico .NET

Os modelos de serviço de trabalho criam um host genérico .NET, <xref:Microsoft.Extensions.Hosting.HostBuilder> . O host genérico pode ser usado com outros tipos de aplicativos .NET, como aplicativos de console.

Um *host* é um objeto que encapsula os recursos de um aplicativo, tais como:

- DI (injeção de dependência)
- Log
- Configuração
- Implementações de `IHostedService`

Quando um host é iniciado, ele chama <xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync%2A?displayProperty=nameWithType> cada implementação de <xref:Microsoft.Extensions.Hosting.IHostedService> registrado na coleção de serviços hospedados do contêiner de serviço. Em um aplicativo de serviço de trabalho, todas as `IHostedService` implementações que contêm <xref:Microsoft.Extensions.Hosting.BackgroundService> instâncias têm seus <xref:Microsoft.Extensions.Hosting.BackgroundService.ExecuteAsync%2A?displayProperty=nameWithType> métodos chamados.

O principal motivo para incluir todos os recursos interdependentes do aplicativo em um objeto é o gerenciamento de tempo de vida: controle sobre a inicialização do aplicativo e desligamento normal. Isso é obtido com o pacote NuGet [Microsoft. Extensions. Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting) .

## <a name="set-up-a-host"></a>Configurar um host

O host normalmente é configurado, compilado e executado pelo código na classe `Program`. O método `Main`:

- Chama um método <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder> para criar e configurar um objeto construtor.
- Chamadas <xref:Microsoft.Extensions.Hosting.IHostBuilder.Build> para criar uma <xref:Microsoft.Extensions.Hosting.IHost> instância.
- Chamadas <xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Run%2A> ou <xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.RunAsync%2A> método no objeto de host.

Os modelos de serviço do .NET Worker geram o seguinte código para criar um host genérico:

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureServices((hostContext, services) =>
            {
                services.AddHostedService<Worker>();
            });
}
```

## <a name="default-builder-settings"></a>Configurações do construtor padrão

O método <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder%2A>:

- Define a raiz do conteúdo como o caminho retornado por <xref:System.IO.Directory.GetCurrentDirectory>.
- Carrega a [configuração do host](#host-configuration) de:
  - Variáveis de ambiente prefixadas com `DOTNET_` .
  - Argumentos de linha de comando.
- Carrega a configuração do aplicativo de:
  - *appsettings.jsem*.
  - *appsettings.{Environment}.json*.
  - Gerenciador de Segredo quando o aplicativo é executado no ambiente `Development`.
  - Variáveis de ambiente.
  - Argumentos de linha de comando.
- Adiciona os seguintes provedores de registro em log:
  - Console
  - Depurar
  - EventSource
  - EventLog (somente quando em execução no Windows)
- Habilita validação de escopo e [validação de dependência](xref:Microsoft.Extensions.DependencyInjection.ServiceProviderOptions.ValidateOnBuild) quando o ambiente é `Development` .

O `ConfigureServices` método expõe a capacidade de adicionar serviços à <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection?displayProperty=nameWithType> instância. Posteriormente, esses serviços podem ser disponibilizados da injeção de dependência.

## <a name="framework-provided-services"></a>Serviços fornecidos pela estrutura

Os seguintes serviços são registrados automaticamente:

- [IHostApplicationLifetime](#ihostapplicationlifetime)
- [IHostLifetime](#ihostlifetime)
- [IHostEnvironment](#ihostenvironment)

## <a name="ihostapplicationlifetime"></a>IHostApplicationLifetime

Injetar o <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime> serviço em qualquer classe para lidar com tarefas de desligamento de inicialização e de fechamento normal. Três propriedades na interface são tokens de cancelamento usados para registrar métodos de manipulador de eventos de inicialização e desligamento do aplicativo. A interface também inclui um método <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime.StopApplication>.

O exemplo a seguir é uma `IHostedService` implementação que registra `IHostApplicationLifetime` eventos:

:::code language="csharp" source="snippets/configuration/app-lifetime/ExampleHostedService.cs" highlight="18-20":::

O modelo de serviço de trabalho pode ser modificado para adicionar a `ExampleHostedService` implementação:

:::code language="csharp" source="snippets/configuration/app-lifetime/Program.cs" range="1-16,36" highlight="15":::

O aplicativo gravaria a seguinte saída de exemplo:

:::code language="csharp" source="snippets/configuration/app-lifetime/Program.cs" range="17-35":::

## <a name="ihostlifetime"></a>IHostLifetime

A implementação <xref:Microsoft.Extensions.Hosting.IHostLifetime> controla quando o host é iniciado e quando ele é interrompido. A última implementação registrada é usada.

`Microsoft.Extensions.Hosting.Internal.ConsoleLifetime` é a implementação `IHostLifetime` padrão. `ConsoleLifetime`:

- Escuta <kbd>Ctrl</kbd> + <kbd>C</kbd>, [SIGINT](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGINT)ou [SIGTERM](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGTERM) e chama <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime.StopApplication%2A> para iniciar o processo de desligamento.
- Desbloqueia extensões como `RunAsync` e `WaitForShutdownAsync` .

## <a name="ihostenvironment"></a>IHostEnvironment

Insira o <xref:Microsoft.Extensions.Hosting.IHostEnvironment> serviço em uma classe para obter informações sobre as seguintes configurações:

- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ApplicationName?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ContentRootFileProvider?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ContentRootPath?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.EnvironmentName?displayProperty=nameWithType>

## <a name="host-configuration"></a>Configuração do host

A configuração do host é usada para configurar as propriedades da implementação do [IHostEnvironment](#ihostenvironment) .

A configuração do host está disponível em [HostBuilderContext.Configuração](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration) dentro do <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration%2A> método. Ao chamar o `ConfigureAppConfiguration` método, `HostBuilderContext` e `IConfigurationBuilder` são passados para o `configureDelegate` . O `configureDelegate` é definido como um `Action<HostBuilderContext, IConfigurationBuilder>` . O contexto do construtor de hosts expõe a `.Configuration` propriedade, que é uma instância do `IConfiguration` . Ele representa a configuração criada a partir do host, enquanto o `IConfigurationBuilder` é o objeto do construtor usado para configurar o aplicativo.

> [!TIP]
> After `ConfigureAppConfiguration` é chamado de `HostBuilderContext.Configuration` é substituído pela [configuração do aplicativo](#app-configuration).

Para adicionar a configuração do host, chame <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureHostConfiguration%2A> em `IHostBuilder`. `ConfigureHostConfiguration` pode ser chamado várias vezes com resultados aditivos. O host usa a opção que define um valor por último em uma chave determinada.

O exemplo a seguir cria a configuração de host:

:::code language="csharp" source="snippets/configuration/console-host/Program.cs" highlight="19-25":::

## <a name="app-configuration"></a>Configuração de aplicativo

A configuração de aplicativo é criada chamando <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration%2A> em `IHostBuilder`. `ConfigureAppConfiguration` pode ser chamado várias vezes com resultados aditivos. O aplicativo usa a opção que define um valor por último em uma chave determinada.

A configuração criada pelo `ConfigureAppConfiguration` está disponível em [HostBuilderContext.Configuração](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration%2A) para operações subsequentes e como um serviço de di. A configuração do host também é adicionada à configuração do aplicativo.

Para obter mais informações, consulte [Configuration in .net](configuration.md).

## <a name="see-also"></a>Veja também

- [Configuração no .NET](configuration.md)
- [Host da Web do ASP.NET Core](/aspnet/core/fundamentals/host/web-host)
- Os bugs de host genéricos devem ser criados no repositório [github.com/dotnet/Extensions](https://github.com/dotnet/extensions/issues)
