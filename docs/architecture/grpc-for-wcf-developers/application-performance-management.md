---
title: Gerenciamento de desempenho de aplicativos-gRPC para desenvolvedores do WCF
description: Registro em log, métricas e rastreamento para aplicativos ASP.NET Core gRPC.
ms.date: 12/15/2020
ms.openlocfilehash: 8a2a89e268e3b2dffdcc945ac71b2de85b4d4964
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938449"
---
# <a name="application-performance-management"></a>Gerenciamento de desempenho de aplicativos

Em ambientes de produção como o kubernetes, é importante monitorar os aplicativos para garantir que eles estejam sendo executados de forma ideal. O registro em log e as métricas são importantes em particular. ASP.NET Core, incluindo o gRPC, fornece suporte interno para produzir e gerenciar mensagens de log e dados de métrica, bem como dados de *rastreamento* .

## <a name="the-difference-between-logging-and-metrics"></a>A diferença entre registro em log e métricas

O *registro em log* se preocupa com mensagens de texto que registram informações detalhadas sobre as coisas ocorridas no sistema. As mensagens de log podem incluir dados de exceção, como rastreamentos de pilha ou dados estruturados que fornecem contexto sobre a mensagem. A saída de log é normalmente gravada em um repositório de texto pesquisável.

As *métricas* referem-se aos dados numéricos projetados para serem agregados e apresentados usando gráficos em um painel. O painel fornece uma visão geral da integridade e do desempenho de um aplicativo. Os dados de métricas também podem ser usados para disparar alertas automatizados quando um limite é excedido. Aqui estão alguns exemplos de dados de métricas:

- Tempo necessário para processar solicitações.
- O número de solicitações por segundo manipuladas por uma instância de um serviço.
- O número de solicitações com falha em uma instância.

## <a name="logging-in-aspnet-core-grpc"></a>Fazendo logon ASP.NET Core gRPC

O ASP.NET Core fornece suporte interno para registro em log, na forma do pacote NuGet [Microsoft. Extensions. Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging) . As principais partes dessa biblioteca estão incluídas no SDK da Web, portanto, não é necessário instalá-las manualmente. Por padrão, as mensagens de log são gravadas na saída padrão (o "console") e em qualquer depurador anexado. Para gravar logs em armazenamentos de dados externos persistentes, talvez seja necessário importar [pacotes de coletor de log opcionais](/aspnet/core/fundamentals/logging/?view=aspnetcore-3.0#third-party-logging-providers).

O ASP.NET Core estrutura gRPC grava mensagens de log de diagnóstico detalhadas para essa estrutura de log, para que elas possam ser processadas e armazenadas junto com as próprias mensagens do seu aplicativo.

### <a name="produce-log-messages"></a>Produzir mensagens de log

A extensão de log é automaticamente registrada com o sistema de injeção de dependência ASP.NET Core, para que você possa especificar os agentes como um parâmetro de Construtor em tipos de serviço gRPC.

```csharp
public class StockData : Stocks.StocksBase
{
    private readonly ILogger<StockData> _logger;

    public StockData(ILogger<StockData> logger)
    {
        _logger = logger;
    }
}
```

Muitas mensagens de log, como solicitações e exceções, são fornecidas pelos componentes ASP.NET Core e gRPC Framework. Adicione suas próprias mensagens de log para fornecer detalhes e contexto sobre a lógica do aplicativo, em vez de preocupações de nível inferior.

Para obter mais informações sobre como gravar mensagens de log e destinos e coletores de log disponíveis, consulte  [Logging in .NET Core and ASP.NET Core](/aspnet/core/fundamentals/logging/).

## <a name="metrics-in-aspnet-core-grpc"></a>Métricas no ASP.NET Core gRPC

O tempo de execução do .NET Core fornece um conjunto de componentes para emitir e observar métricas. Isso inclui APIs como as <xref:System.Diagnostics.Tracing.EventSource> classes e <xref:System.Diagnostics.Tracing.EventCounter> . Essas APIs podem emitir dados numéricos básicos que podem ser consumidos por processos externos, como a [ferramenta global dotnet-Counters](../../core/diagnostics/dotnet-counters.md)ou o rastreamento de eventos para Windows. Para obter mais informações sobre como usar `EventCounter` o em seu próprio código, consulte [introdução ao EventCounter](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.Tracing/documentation/EventCounterTutorial.md).

Para obter métricas mais avançadas e gravar dados de métrica em uma maior variedade de armazenamentos de dados, você pode tentar um projeto de código-fonte aberto chamado [métricas de aplicativo](https://www.app-metrics.io). Esse conjunto de bibliotecas fornece um amplo conjunto de tipos para instrumentar seu código. Ele também oferece pacotes para gravar métricas em diferentes tipos de destinos que incluem bancos de dados de série temporal, como Prometheus e InfluxDB, e [Application insights](/azure/azure-monitor/app/app-insights-overview). O pacote NuGet [app. Metrics. AspNetCore. Mvc](https://www.nuget.org/packages/App.Metrics.AspNetCore.Mvc/) , inclusive, adiciona um conjunto abrangente de métricas básicas que são geradas automaticamente por meio da integração com o ASP.NET Core Framework. O site do projeto fornece [modelos](https://www.app-metrics.io/samples/grafana/) para exibir essas métricas com a plataforma de visualização [Grafana](https://grafana.com/) .

### <a name="produce-metrics"></a>Produzir métricas

A maioria das plataformas de métricas oferece suporte aos seguintes tipos:

| Tipo de métrica | Descrição |
| ----------- | ----------- |
| Contador     | Controla com que frequência algo acontece, como solicitações e erros. |
| Medidor       | Registra um único valor que muda ao longo do tempo, como conexões ativas. |
| Histograma   | Mede uma distribuição de valores entre limites arbitrários. Por exemplo, um histograma pode acompanhar o tamanho do conjunto de registros, contando quantas continham os 10 <, quantos registros continham 11-100, quantos registros de 101-1000 continham e quantas continham >1000 registros. |
| Medidor       | Mede a taxa na qual um evento ocorre em vários intervalos de tempo. |
| Temporizador       | Controla a duração de eventos e a taxa na qual ele ocorre, armazenado como um histograma. |

Usando as *métricas de aplicativo*, uma `IMetrics` interface pode ser obtida por meio de injeção de dependência e usada para registrar qualquer uma dessas métricas para um serviço gRPC. O exemplo a seguir mostra como contar o número de `Get` solicitações feitas ao longo do tempo:

```csharp
public class StockData : Stocks.StocksBase
{
    private static readonly CounterOptions GetRequestCounter = new CounterOptions
    {
        Name = "StockData_Get_Requests",
        MeasurementUnit = Unit.Calls
    };

    private readonly IStockRepository _repository;
    private readonly IMetrics _metrics;

    public StockData(IStockRepository repository, IMetrics metrics)
    {
        _repository = repository;
        _metrics = metrics;
    }

    public override async Task<GetResponse> Get(GetRequest request, ServerCallContext context)
    {
        _metrics.Measure.Counter.Increment(GetRequestCounter);

        // Serve request...
    }
}
```

### <a name="store-and-visualize-metrics-data"></a>Armazenar e Visualizar dados de métricas

A melhor maneira de armazenar dados de métricas está em um banco de dados de série temporal, um armazenamento de dado especializado criado para registrar séries de dados numéricas marcadas com carimbos de data */hora*. Os bancos de dados mais populares são [Prometheus](https://prometheus.io/) e [InfluxDB](https://www.influxdata.com/products/influxdb-overview/). O Microsoft Azure também fornece armazenamento de métricas dedicado por meio do serviço de [Azure monitor](/azure/azure-monitor/overview) .

A solução atual para visualização de dados de métricas é [Grafana](https://grafana.com), que funciona com uma ampla variedade de provedores de armazenamento. A imagem a seguir mostra um painel Grafana de exemplo que exibe as métricas da malha do serviço Linkerd que executa o exemplo StockData:

![Captura de tela do painel do Grafana](media/application-performance-management/grafana-screenshot.png)

### <a name="metrics-based-alerting"></a>Alertas baseados em métricas

A natureza numérica dos dados de métricas significa que ele é ideal para impulsionar sistemas de alerta, notificando os desenvolvedores ou engenheiros de suporte quando um valor cai fora de alguma tolerância definida. Todas as plataformas já mencionadas fornecem suporte para alertas por meio de uma variedade de opções, incluindo emails, mensagens de texto ou visualizações no painel.

## <a name="distributed-tracing"></a>Rastreamento distribuído

O rastreamento distribuído é um desenvolvimento relativamente recente no monitoramento, que tem surgido do uso crescente de microserviços e arquiteturas distribuídas. Uma única solicitação de um navegador cliente, aplicativo ou dispositivo pode ser dividida em várias etapas e subsolicitaçãos e envolve o uso de muitos serviços em uma rede. Essa atividade dificulta a correlação de mensagens de log e métricas com a solicitação específica que as disparou. O rastreamento distribuído aplica identificadores a solicitações e permite que os logs e as métricas sejam correlacionados a uma operação específica. Esse rastreamento é semelhante ao [rastreamento de ponta a ponta do WCF](../../framework/wcf/diagnostics/tracing/end-to-end-tracing.md), mas é aplicado em várias plataformas.

O rastreamento distribuído cresceu rapidamente em popularidade e está começando a padronizar. A base de computação nativa da nuvem criou o [padrão de rastreamento aberto](https://opentracing.io), tentando fornecer bibliotecas neutras ao fornecedor para trabalhar com back-ends, como [Jaeger](https://www.jaegertracing.io/) e o [APM elástico](https://www.elastic.co/products/apm). Ao mesmo tempo, o Google criou o [projeto OpenCensus](https://opencensus.io/) para abordar o mesmo conjunto de problemas. Esses dois projetos estão se mesclando em um novo projeto, [OpenTelemetry](https://opentelemetry.io), que visa ser o padrão do setor do futuro.

### <a name="how-distributed-tracing-works"></a>Como funciona o rastreamento distribuído

O rastreamento distribuído baseia-se no conceito de *spans*: operações nomeadas e oportunas que fazem parte de um único *rastreamento*, o que pode envolver o processamento em vários nós de um sistema. Quando uma nova operação é iniciada, um rastreamento é criado com um identificador exclusivo. Para cada suboperação, um Span é criado com seu próprio identificador e identificador de rastreamento. À medida que a solicitação passa pelo sistema, vários componentes podem criar spans *filho* que incluem o identificador de seu *pai*. Um Span tem um *contexto*, que contém os identificadores de rastreamento e de span, bem como dados úteis na forma de pares de chave e valor (chamados de *bagagem*).

### <a name="distributed-tracing-with-diagnosticsource"></a>Rastreamento distribuído com `DiagnosticSource`

O .NET tem um módulo interno que mapeia bem para rastreamentos e spans distribuídos: [diagnosticname](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md#diagnosticsource-users-guide). Além de fornecer uma maneira simples de produzir e consumir diagnósticos em um processo, o `DiagnosticSource` módulo tem o conceito de uma *atividade*. Uma atividade é efetivamente uma implementação de um rastreamento distribuído ou um intervalo dentro de um rastreamento. Os elementos internos do módulo cuidam das atividades pai/filho, incluindo a alocação de identificadores. Para obter mais informações sobre como usar o `Activity` tipo, consulte o [Guia do usuário da atividade no GitHub](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md#activity-user-guide).

Como `DiagnosticSource` o é uma parte da estrutura principal e posterior, ele tem suporte por vários componentes principais. Eles incluem <xref:System.Net.Http.HttpClient> , Entity Framework Core e ASP.NET Core, incluindo o suporte explícito na estrutura gRPC. Quando ASP.NET Core recebe uma solicitação, ele verifica um par de cabeçalhos HTTP que correspondem ao padrão de [contexto de rastreamento W3C](https://www.w3.org/TR/trace-context) . Se os cabeçalhos forem encontrados, uma atividade será iniciada usando os valores de identidade e o contexto dos cabeçalhos. Se nenhum cabeçalho for encontrado, uma atividade será iniciada com valores de identidade gerados que correspondam ao formato padrão. Qualquer diagnóstico gerado pela estrutura ou pelo código do aplicativo durante o tempo de vida dessa atividade pode ser marcado com os identificadores de rastreamento e span. O `HttpClient` suporte estende essa funcionalidade ainda mais verificando se há uma atividade atual em cada solicitação e adicionando automaticamente os cabeçalhos de rastreamento à solicitação de saída.

As bibliotecas de cliente e servidor do ASP.NET Core gRPC incluem suporte explícito para `DiagnosticSource` e e `Activity` criam atividades, e aplicam e usam informações de cabeçalho automaticamente.

> [!NOTE]
> Tudo isso ocorre apenas se um ouvinte estiver consumindo as informações de diagnóstico. Se não houver um ouvinte, nenhum diagnóstico será gravado e nenhuma atividade será criada.

### <a name="add-your-own-diagnosticsource-and-activity"></a>Adicione seu próprio `DiagnosticSource` e `Activity`

Para adicionar seu próprio diagnóstico ou criar spans explícitos dentro do código do aplicativo, consulte o [Guia do usuário do diagnosticm](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md#instrumenting-with-diagnosticsourcediagnosticlistener) e o [Guia do usuário da atividade](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md#activity-usage).

### <a name="store-distributed-trace-data"></a>Armazenar dados de rastreamento distribuído

No momento da gravação, o projeto OpenTelemetry ainda está nos estágios iniciais e somente os pacotes de qualidade alfa estão disponíveis para aplicativos .NET. O projeto OpenTracing atualmente oferece bibliotecas mais maduras.

A API OpenTracing é descrita na seção a seguir. Se você quiser usar a API OpenTelemetry em seu aplicativo em vez disso, consulte o [repositório do SDK do .net do OpenTelemetry](https://github.com/open-telemetry/opentelemetry-dotnet) no github.

#### <a name="use-the-opentracing-package-to-store-distributed-trace-data"></a>Usar o pacote OpenTracing para armazenar dados de rastreamento distribuídos

O [pacote NuGet OpenTracing](https://www.nuget.org/packages/OpenTracing/) dá suporte a todos os back-ends compatíveis com OpenTracing (que podem ser usados independentemente de `DiagnosticSource` ). Há um pacote adicional do projeto de contribuições da API do OpenTracing, [OpenTracing. contrib. NetCore](https://www.nuget.org/packages/OpenTracing.Contrib.NetCore/). Esse pacote adiciona um `DiagnosticSource` ouvinte e grava eventos e atividades em um back-end automaticamente. Habilitar esse pacote é tão simples quanto instalá-lo do NuGet e adicioná-lo como um serviço em sua `Startup` classe.

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddOpenTracing();
    }
}
```

O pacote OpenTracing é uma camada de abstração e, como tal, requer implementação específica para o back-end. As implementações da API OpenTracing estão disponíveis para os seguintes back-ends de software livre.

| Nome | Pacote | Site da Web |
| ---- | ------- | -------- |
| Jaeger | [Jaeger](https://www.nuget.org/packages/Jaeger/) | [jaegertracing.io](https://jaegertracing.io) |
| APM elástico | [Elástico. APM. NetCoreAll](https://www.nuget.org/packages/Elastic.Apm.NetCoreAll/) | [elastic.co/products/apm](https://www.elastic.co/products/apm) |

Para obter mais informações sobre a API do OpenTracing para .NET, consulte os repositórios [OpenTracing for c#](https://github.com/opentracing/opentracing-csharp) e [OpenTracing contrib C#/.NET Core](https://github.com/opentracing-contrib/csharp-netcore) no github.

>[!div class="step-by-step"]
>[Anterior](load-balancing.md) 
> [Avançar](appendix.md)
