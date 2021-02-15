---
title: Provedores de log no .NET
description: Saiba como a API do provedor de log é usada em aplicativos .NET.
author: IEvangelist
ms.author: dapine
ms.date: 12/04/2020
ms.openlocfilehash: fdec9018e58c6038b5589c01e775bbb5f10b6b10
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740086"
---
# <a name="logging-providers-in-net"></a>Provedores de log no .NET

Os provedores de log mantêm logs, exceto para o `Console` provedor, que exibe apenas os logs como saída padrão. Por exemplo, o provedor do Aplicativo Azure insights armazena logs no Aplicativo Azure insights. Vários provedores podem ser habilitados.

Os modelos de aplicativo do .NET Worker padrão:

- Use o [host genérico](generic-host.md).
- Chamada <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder%2A> , que adiciona os seguintes provedores de log:
  - [Console](#console)
  - [Depurar](#debug)
  - [EventSource](#event-source)
  - [EventLog](#windows-eventlog): somente Windows

:::code language="csharp" source="snippets/configuration/console/Program.cs" highlight="18":::

O código anterior mostra a `Program` classe criada com os modelos de aplicativo do .net Worker. As várias seções a seguir fornecem exemplos baseados nos modelos de aplicativo do .NET Worker, que usam o host genérico.

Para substituir o conjunto padrão de provedores de log adicionados pelo `Host.CreateDefaultBuilder` , chame `ClearProviders` e adicione os provedores de log que você deseja. Por exemplo, o código a seguir:

- Chama <xref:Microsoft.Extensions.Logging.LoggingBuilderExtensions.ClearProviders%2A> para remover todas as <xref:Microsoft.Extensions.Logging.ILoggerProvider> instâncias do construtor.
- Adiciona o provedor de log de [console](#console) .

```csharp
static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureLogging(logging =>
        {
            logging.ClearProviders();
            logging.AddConsole();
        });
```

Para provedores adicionais, consulte:

- [Provedores de log internos](#built-in-logging-providers).
- [Provedores de log de](#third-party-logging-providers)terceiros.

## <a name="configure-a-service-that-depends-on-ilogger"></a>Configurar um serviço que depende do ILogger

Para configurar um serviço que depende do `ILogger<T>` , use a injeção de construtor ou forneça um método de fábrica. A abordagem do método de fábrica é recomendada somente se não há nenhuma outra opção. Por exemplo, considere um serviço que precisa de uma `ILogger<T>` instância fornecida por di:

```csharp
.ConfigureServices(services =>
    services.AddSingleton<IExampleService>(container =>
        new DefaultExampleService
        {
            Logger = container.GetRequiredService<ILogger<IExampleService>>()
        }));
```

O código anterior é um [Func<IServiceProvider, IExampleService>](/dotnet/api/system.func-2) que é executado pela primeira vez que o contêiner di precisa construir uma instância do `IExampleService` . Você pode acessar qualquer um dos serviços registrados dessa maneira.

## <a name="built-in-logging-providers"></a>Provedores de log internos

As extensões da Microsoft incluem os seguintes provedores de log como parte das bibliotecas de tempo de execução:

- [Console](#console)
- [Depurar](#debug)
- [EventSource](#event-source)
- [EventLog](#windows-eventlog)

Os provedores de log a seguir são fornecidos pela Microsoft, mas não como parte das bibliotecas de tempo de execução. Eles devem ser instalados como pacotes NuGet adicionais.

- [AzureAppServicesFile e AzureAppServicesBlob](#azure-app-service)
- [ApplicationInsights](#azure-application-insights)

### <a name="console"></a>Console

O `Console` provedor registra a saída no console.

### <a name="debug"></a>Depurar

O `Debug` provedor grava a saída de log usando a classe [System. Diagnostics. Debug](/dotnet/api/system.diagnostics.debug) . Chamadas para `System.Diagnostics.Debug.WriteLine` gravar no `Debug` provedor.

No Linux, o `Debug` local do log do provedor é dependente de distribuição e pode ser um dos seguintes:

- */var/log/message*
- */var/log/syslog*

### <a name="event-source"></a>Origem do Evento

O `EventSource` provedor grava em uma origem de evento de plataforma cruzada com o nome `Microsoft-Extensions-Logging` . No Windows, o provedor usa o [ETW](/windows/win32/etw/event-tracing-portal).

#### <a name="dotnet-trace-tooling"></a>ferramentas de rastreamento dotnet

A ferramenta [dotnet-Trace](../diagnostics/dotnet-trace.md) é uma ferramenta global da CLI de plataforma cruzada que habilita a coleta de rastreamentos do .NET Core de um processo em execução. A ferramenta coleta <xref:Microsoft.Extensions.Logging.EventSource> dados do provedor usando um <xref:Microsoft.Extensions.Logging.EventSource.LoggingEventSource> .

Consulte [dotnet-Trace](../diagnostics/dotnet-trace.md) para obter instruções de instalação. Para obter um tutorial de diagnóstico usando o `dotnet-trace` , consulte [debug High CPU Usage in .NET Core](../diagnostics/debug-highcpu.md).

### <a name="windows-eventlog"></a>EventLog do Windows

O `EventLog` provedor envia a saída de log para o log de eventos do Windows. Ao contrário dos outros provedores, o `EventLog` provedor ***não** herda as configurações padrão de não provedor. Se `EventLog` as configurações de log não forem especificadas, elas serão padronizadas como padrão `LogLevel.Warning` .

Para registrar em log eventos inferiores <xref:Microsoft.Extensions.Logging.LogLevel.Warning?displayProperty=nameWithType> a, defina explicitamente o nível de log. O exemplo a seguir define o nível de log padrão do log de eventos como <xref:Microsoft.Extensions.Logging.LogLevel.Information?displayProperty=nameWithType> :

```json
"Logging": {
  "EventLog": {
    "LogLevel": {
      "Default": "Information"
    }
  }
}
```

[Sobrecargas de autoeventlog](xref:Microsoft.Extensions.Logging.EventLoggerFactoryExtensions) podem passar <xref:Microsoft.Extensions.Logging.EventLog.EventLogSettings> . Se `null` ou não for especificado, as seguintes configurações padrão serão usadas:

- `LogName`: "Aplicativo"
- `SourceName`: "Tempo de execução do .NET"
- `MachineName`: O nome do computador local é usado.

O código a seguir altera o `SourceName` do valor padrão de `".NET Runtime"` para `CustomLogs` :

```csharp
public class Program
{
    static async Task Main(string[] args)
    {
        using IHost host = CreateHostBuilder(args).Build();

        // Application code should start here.

        await host.RunAsync();
    }

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
                logging.AddEventLog(configuration =>
                    configuration.SourceName = "CustomLogs"));
}
```

### <a name="azure-app-service"></a>Serviço de aplicativo do Azure

O pacote de provedor [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) grava logs em arquivos de texto no sistema de arquivos de um aplicativo do Serviço de Aplicativo do Azure e no [armazenamento de blobs](/azure/storage/blobs/storage-quickstart-blobs-dotnet#what-is-blob-storage) em uma conta de Armazenamento do Azure.

O pacote do provedor não está incluído nas bibliotecas de tempo de execução. Para usar o provedor, adicione o pacote do provedor ao projeto.

Para definir as configurações do provedor, use <xref:Microsoft.Extensions.Logging.AzureAppServices.AzureFileLoggerOptions> e <xref:Microsoft.Extensions.Logging.AzureAppServices.AzureBlobLoggerOptions>, conforme mostrado no exemplo a seguir:

```csharp
class Program
{
    static async Task Main(string[] args)
    {
        using IHost host = CreateHostBuilder(args).Build();

        // Application code should start here.

        await host.RunAsync();
    }

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
                logging.AddAzureWebAppDiagnostics())
            .ConfigureServices(services =>
                services.Configure<AzureFileLoggerOptions>(options =>
                {
                    options.FileName = "azure-diagnostics-";
                    options.FileSizeLimit = 50 _ 1024;
                    options.RetainedFileCountLimit = 5;
                })
                .Configure<AzureBlobLoggerOptions>(options =>
                {
                    options.BlobName = "log.txt";
                }));
}
```

Quando implantado no serviço Azure App, o aplicativo usa as configurações na seção [logs do serviço de aplicativo](/azure/app-service/web-sites-enable-diagnostic-log/#enable-application-logging-windows) da página Serviço de **aplicativo** da portal do Azure. Quando as configurações a seguir são atualizadas, as alterações entram em vigor imediatamente sem a necessidade de uma reinicialização ou reimplantação do aplicativo.

- **Log de aplicativo (Sistema de Arquivos)**
- **Log de aplicativo (Blob)**

O local padrão para arquivos de log é na pasta *D:\\home\\LogFiles\\Application* e o nome de arquivo padrão é *diagnostics-aaaammdd.txt*. O limite padrão de tamanho do arquivo é 10 MB e o número padrão máximo de arquivos mantidos é 2. O nome de blob padrão é *{app-name}{timestamp}/aaaa/mm/dd/hh/{guid}-applicationLog.txt*.

Esse provedor só registra quando o projeto é executado no ambiente do Azure.

#### <a name="azure-log-streaming"></a>Fluxo de log do Azure

O Azure log streaming dá suporte à exibição da atividade de log em tempo real em:

- O servidor de aplicativos
- Do servidor Web
- De uma solicitação de rastreio com falha

Para configurar o fluxo de log do Azure:

- Navegue até a página de **logs do serviço de aplicativo** na página do portal do aplicativo.
- Defina **Habilitar o log de aplicativo (sistema de arquivos)** como **Ativada**.
- Escolha o **Nível** de log. Essa configuração se aplica somente ao streaming de log do Azure.

Navegue até a página **fluxo de log** para exibir os logs. As mensagens registradas são registradas com a `ILogger` interface.

### <a name="azure-application-insights"></a>Azure Application Insights

O pacote do provedor [Microsoft. Extensions. Logging. ApplicationInsights](https://www.nuget.org/packages/Microsoft.Extensions.Logging.ApplicationInsights) grava logs em [aplicativo Azure insights](/azure/azure-monitor/app/cloudservices). O Application Insights é um serviço que monitora um aplicativo web e fornece ferramentas para consultar e analisar os dados de telemetria. Se você usar esse provedor, poderá consultar e analisar os logs usando as ferramentas do Application Insights.

Para obter mais informações, consulte os seguintes recursos:

- [Visão geral do Application Insights](/azure/application-insights/app-insights-overview)
- [ApplicationInsightsLoggerProvider para logs do .NET Core ILogger](/azure/azure-monitor/app/ilogger) – Comece aqui se você quiser implementar o provedor de log sem o restante da telemetria do Application Insights.
- [Application Insights logging adapters](/azure/azure-monitor/app/asp-net-trace-logs) (Adaptadores de registro em log do Application Insights).
- [Instalar, configurar e inicializar o SDK do Application Insights](/learn/modules/instrument-web-app-code-with-application-insights) – Tutorial interativo no site da Microsoft Learn.

## <a name="third-party-logging-providers"></a>Provedores de log de terceiros

Aqui estão algumas estruturas de log de terceiros que funcionam com várias cargas de trabalho .NET:

- [elmah.io](https://elmah.io) ([repositório GitHub](https://github.com/elmahio/Elmah.Io.Extensions.Logging))
- [Gelf](https://docs.graylog.org/en/2.3/pages/gelf.html) ([repositório do GitHub](https://github.com/mattwcole/gelf-extensions-logging))
- [JSNLog](http://jsnlog.com) ([repositório GitHub](https://github.com/mperdeck/jsnlog))
- [KissLog.net](https://kisslog.net) ([Repositório do GitHub](https://github.com/catalingavan/KissLog-net))
- [Log4net](https://logging.apache.org/log4net) ([repositório GitHub](https://github.com/apache/logging-log4net))
- [Loggr](https://loggr.net) ([repositório GitHub](https://github.com/imobile3/Loggr.Extensions.Logging))
- [NLog](https://nlog-project.org) ([repositório GitHub](https://github.com/NLog/NLog.Extensions.Logging))
- [Sentry](https://sentry.io/welcome) ([repositório GitHub](https://github.com/getsentry/sentry-dotnet))
- [Serilog](https://serilog.net) ([repositório GitHub](https://github.com/serilog/serilog-sinks-console))
- [Stackdriver](https://cloud.google.com/dotnet/docs/stackdriver#logging) ([repositório GitHub](https://github.com/googleapis/google-cloud-dotnet))

Algumas estruturas de terceiros podem fazer o [log semântico, também conhecido como registro em log estruturado](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).

Usar uma estrutura de terceiros é semelhante ao uso de um dos provedores internos:

1. Adicione um pacote NuGet ao projeto.
1. Chame um `ILoggerFactory` `ILoggingBuilder` método de extensão ou fornecido pela estrutura de log.

Para saber mais, consulte a documentação de cada provedor. Não há suporte para provedores de log de terceiros na Microsoft.

## <a name="see-also"></a>Confira também

- [Registro em log no .net](logging.md).
- [Implemente um provedor de log personalizado no .net](custom-logging-provider.md).
- [Registro em log de alto desempenho no .net](high-performance-logging.md).
