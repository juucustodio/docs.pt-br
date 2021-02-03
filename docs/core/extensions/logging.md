---
title: Registro em log no .NET
author: IEvangelist
description: Saiba como usar a estrutura de registro em log fornecida pelo pacote do NuGet Microsoft.Extensions.Logging.
ms.author: dapine
ms.date: 09/30/2020
ms.openlocfilehash: 80695558cabb741bc25e7fe2650d4a99f9c25c1f
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505622"
---
# <a name="logging-in-net"></a>Registro em log no .NET

O .NET oferece suporte a uma API de log que funciona com uma variedade de provedores de log internos e de terceiros. Este artigo mostra como usar a API de registro em log com provedores internos. A maioria dos exemplos de código mostrados neste artigo se aplica a qualquer aplicativo .NET que usa o [host genérico](generic-host.md). Para aplicativos que não usam o host genérico, consulte [aplicativo de console que não](#non-host-console-app)é de host.

## <a name="create-logs"></a>Criar logs

Para criar logs, use um <xref:Microsoft.Extensions.Logging.ILogger%601> objeto da [injeção de dependência (di)](dependency-injection.md).

O exemplo a seguir:

- Cria um agente, `ILogger<Worker>` , que usa uma *categoria* de log do nome totalmente qualificado do tipo `Worker` . A categoria do log é uma cadeia de caracteres associada a cada log.
- Chamadas <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation%2A> para log no `Information` nível. O *nível* de log indica a gravidade do evento registrado.

:::code language="csharp" source="snippets/configuration/worker-service/Worker.cs" range="9-24" highlight="12":::

[Níveis](#log-level) e [categorias](#log-category) serão explicados com mais detalhes posteriormente neste artigo.

## <a name="configure-logging"></a>Configurar o registro em log

A configuração de log é normalmente fornecida pela `Logging` seção de *appSettings*. `{Environment}` arquivos *. JSON* . O seguinte *appsettings.Development.jsno* arquivo é gerado pelos modelos de serviço do .net Worker:

:::code language="json" source="snippets/configuration/worker-service/appsettings.Development.json":::

No JSON anterior:

- As `"Default"` `"Microsoft"` categorias,, e `"Microsoft.Hosting.Lifetime"` são especificadas.
- A `"Microsoft"` categoria se aplica a todas as categorias que começam com `"Microsoft"` .
- A `"Microsoft"` categoria registra no nível de log `Warning` e superior.
- A `"Microsoft.Hosting.Lifetime"` categoria é mais específica do que a `"Microsoft"` categoria, portanto, a `"Microsoft.Hosting.Lifetime"` categoria registra em nível de log "informações" e superior.
- Um provedor de log específico não é especificado, portanto `LogLevel` se aplica a todos os provedores de log habilitados, exceto para o [log de eventos do Windows](logging-providers.md#windows-eventlog).

A `Logging` propriedade pode ter <xref:Microsoft.Extensions.Logging.LogLevel> e registrar as propriedades do provedor. O `LogLevel` especifica o [nível](#log-level) mínimo para registrar em log para as categorias selecionadas. No JSON anterior, `Information` e `Warning` os níveis de log são especificados. `LogLevel` indica a severidade do log e varia de 0 a 6:

`Trace` = 0, `Debug` = 1, `Information` = 2, `Warning` = 3, `Error` = 4, `Critical` = 5 e `None` = 6.

Quando um `LogLevel` é especificado, o registro em log é habilitado para mensagens no nível especificado e superior. No JSON anterior, a `Default` categoria é registrada para o `Information` e superior. Por exemplo,,, `Information` `Warning` `Error` e `Critical` as mensagens são registradas em log. Se não `LogLevel` for especificado, o log padrão será o `Information` nível. Para obter mais informações, consulte [níveis de log](#log-level).

Uma propriedade de provedor pode especificar uma `LogLevel` propriedade. `LogLevel` em um provedor especifica os níveis de log para esse provedor e substitui as configurações de log que não são do provedor. Considere o seguinte *appsettings.jsno* arquivo:

:::code language="json" source="snippets/configuration/worker-service/appsettings.Staging.json":::

Configurações em `Logging.{ProviderName}.LogLevel` configurações de substituição no `Logging.LogLevel` . No JSON anterior, o `Debug` nível de log padrão do provedor é definido como `Information` :

`Logging:Debug:LogLevel:Default:Information`

A configuração anterior especifica o `Information` nível de log para cada `Logging:Debug:` categoria, exceto `Microsoft.Hosting` . Quando uma categoria específica é listada, a categoria específica substitui a categoria padrão. No JSON anterior, as `Logging:Debug:LogLevel` categorias `"Microsoft.Hosting"` e `"Default"` substituem as configurações em `Logging:LogLevel`

O nível de log mínimo pode ser especificado para qualquer um dos:

- Provedores específicos: por exemplo, `Logging:EventSource:LogLevel:Default:Information`
- Categorias específicas: por exemplo, `Logging:LogLevel:Microsoft:Warning`
- Todos os provedores e todas as categorias: `Logging:LogLevel:Default:Warning`

Todos os logs abaixo do nível mínimo ***não*** são:

- Passado para o provedor.
- Registrado ou exibido.

Para suprimir todos os logs, especifique [LogLevel. None](xref:Microsoft.Extensions.Logging.LogLevel). `LogLevel.None` tem um valor de 6, que é maior que `LogLevel.Critical` (5).

Se um provedor oferecer suporte a [escopos de log](#log-scopes), `IncludeScopes` indica se eles estão habilitados. Para obter mais informações, consulte [escopos de log](#log-scopes)

O seguinte *appsettings.jsno* arquivo contém configurações para todos os provedores internos:

:::code language="json" source="snippets/configuration/worker-service/appsettings.Production.json":::

Na amostra anterior:

- As categorias e os níveis não são valores sugeridos. O exemplo é fornecido para mostrar todos os provedores padrão.
- Configurações em `Logging.{ProviderName}.LogLevel` configurações de substituição no `Logging.LogLevel` . Por exemplo, o nível em `Debug.LogLevel.Default` substitui o nível em `LogLevel.Default` .
- O *alias* de cada provedor é usado. Cada provedor define um *alias* que pode ser usado na configuração no lugar do nome de tipo totalmente qualificado. Os aliases internos dos provedores são:
  - Console
  - Depurar
  - EventSource
  - EventLog
  - AzureAppServicesFile
  - AzureAppServicesBlob
  - ApplicationInsights

### <a name="set-log-level-by-command-line-environment-variables-and-other-configuration"></a>Definir o nível de log por linha de comando, variáveis de ambiente e outras configurações

O nível de log pode ser definido por qualquer um dos [provedores de configuração](configuration-providers.md).

Os seguintes comandos:

- Defina a chave de ambiente `Logging:LogLevel:Microsoft` para um valor de `Information` no Windows.
- Teste as configurações ao usar um aplicativo criado com os modelos de serviço de trabalho do .NET. O `dotnet run` comando deve ser executado no diretório do projeto depois de usar o `set` .

```cmd
set Logging__LogLevel__Microsoft=Information
dotnet run
```

A configuração de ambiente anterior:

- É definido apenas em processos iniciados na janela de comando em que foram definidos.
- Não é lido por aplicativos iniciados com o Visual Studio.

O comando [setx](/windows-server/administration/windows-commands/setx) a seguir também define a chave de ambiente e o valor no Windows. Ao contrário `set` de, `setx` as configurações são persistidas. A `/M` opção define a variável no ambiente do sistema. Se `/M` não for usado, uma variável de ambiente do usuário será definida.

```cmd
setx Logging__LogLevel__Microsoft=Information /M
```

Em [Azure app serviço](https://azure.microsoft.com/services/app-service/), selecione **nova configuração de aplicativo** na página **configurações > configuração** . Azure App configurações do aplicativo de serviço são:

- Criptografado em repouso e transmitido por um canal criptografado.
- Exposto como variáveis de ambiente.

Para obter mais informações sobre como definir valores de configuração do .NET usando variáveis de ambiente, consulte [variáveis de ambiente](configuration-providers.md#environment-variable-configuration-provider).

## <a name="how-filtering-rules-are-applied"></a>Como as regras de filtragem são aplicadas

Quando um objeto <xref:Microsoft.Extensions.Logging.ILogger%601> é criado, o objeto <xref:Microsoft.Extensions.Logging.ILoggerFactory> seleciona uma única regra por provedor para aplicar a esse agente. Todas as mensagens gravadas pela instância `ILogger` são filtradas com base nas regras selecionadas. A regra mais específica para cada par de provedor e categoria é selecionada nas regras disponíveis.

O algoritmo a seguir é usado para cada provedor quando um `ILogger` é criado para uma determinada categoria:

- Selecione todas as regras que correspondem ao provedor ou seu alias. Se nenhuma correspondência for encontrada, selecione todas as regras com um provedor vazio.
- Do resultado da etapa anterior, selecione as regras com o prefixo de categoria de maior correspondência. Se nenhuma correspondência for encontrada, selecione todas as regras que não especificam uma categoria.
- Se várias regras forem selecionadas, use a **última**.
- Se nenhuma regra for selecionada, use <xref:Microsoft.Extensions.Logging.LoggingBuilderExtensions.SetMinimumLevel(Microsoft.Extensions.Logging.ILoggingBuilder,Microsoft.Extensions.Logging.LogLevel)?displayProperty=nameWithType> para especificar o nível de log mínimo.

## <a name="log-category"></a>Categoria do log

Quando um `ILogger` objeto é criado, uma *categoria* é especificada. Essa categoria é incluída em cada mensagem de log criada por essa instância de `ILogger`. A cadeia de caracteres da categoria é arbitrária, mas a Convenção é usar o nome da classe. Por exemplo, em um aplicativo com um serviço definido como o objeto a seguir, a categoria pode ser `"Example.DefaultService"` :

```csharp
namespace Example
{
    public class DefaultService : IService
    {
        private readonly ILogger<DefaultService> _logger;

        public DefaultService(ILogger<DefaultService> logger) =>
            _logger = logger;

        // ...
    }
}
```

Para especificar explicitamente a categoria, chame <xref:Microsoft.Extensions.Logging.LoggerFactory.CreateLogger%2A?displayProperty=nameWithType>:

```csharp
namespace Example
{
    public class DefaultService : IService
    {
        private readonly ILogger _logger;

        public DefaultService(ILoggerFactory loggerFactory) =>
            _logger = loggerFactory.CreateLogger("CustomCategory");

        // ...
    }
}
```

Chamar `CreateLogger` com um nome fixo pode ser útil quando usado em várias classes/tipos para que os eventos possam ser organizados por categoria.

`ILogger<T>` é equivalente a chamar `CreateLogger` com o nome de tipo totalmente qualificado de `T`.

## <a name="log-level"></a>Nível de log

A tabela a seguir lista os <xref:Microsoft.Extensions.Logging.LogLevel> valores, o `Log{LogLevel}` método de extensão de conveniência e o uso sugerido:

| LogLevel | Valor | Método | Descrição |
|--|--|--|--|
| [Trace](xref:Microsoft.Extensions.Logging.LogLevel) | 0 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogTrace%2A> | Conter as mensagens mais detalhadas. Essas mensagens podem conter dados confidenciais do aplicativo. Essas mensagens são desabilitadas por padrão e ***não*** devem ser habilitadas na produção. |
| [Depurar](xref:Microsoft.Extensions.Logging.LogLevel) | 1 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogDebug%2A> | Para depuração e desenvolvimento. Use com cuidado na produção devido ao alto volume. |
| [Informações](xref:Microsoft.Extensions.Logging.LogLevel) | 2 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation%2A> | Rastreia o fluxo geral do aplicativo. Pode ter um valor de longo prazo. |
| [Aviso](xref:Microsoft.Extensions.Logging.LogLevel) | 3 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogWarning%2A> | Para eventos anormais ou inesperados. Normalmente inclui erros ou condições que não fazem com que o aplicativo falhe. |
| [Erro](xref:Microsoft.Extensions.Logging.LogLevel) | 4 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogError%2A> | Para erros e exceções que não podem ser manipulados. Essas mensagens indicam uma falha na operação ou solicitação atual, não uma falha em todo o aplicativo. |
| [Crítico](xref:Microsoft.Extensions.Logging.LogLevel) | 5 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogCritical%2A> | Para falhas que exigem atenção imediata. Exemplos: cenários de perda de dados, espaço em disco insuficiente. |
| [Nenhuma](xref:Microsoft.Extensions.Logging.LogLevel) | 6 |  | Especifica que nenhuma mensagem deve ser gravada. |

Na tabela anterior, o `LogLevel` é listado da severidade mais baixa para a mais alta.

O primeiro parâmetro do método de [log](xref:Microsoft.Extensions.Logging.LoggerExtensions) , <xref:Microsoft.Extensions.Logging.LogLevel> , indica a severidade do log. Em vez de chamar `Log(LogLevel, ...)` , a maioria dos desenvolvedores chama os métodos de extensão do [log {LogLevel}](xref:Microsoft.Extensions.Logging.LoggerExtensions) . Os `Log{LogLevel}` métodos de extensão [chamam o método de log e especificam o LogLevel](https://github.com/dotnet/extensions/blob/release/3.1/src/Logging/Logging.Abstractions/src/LoggerExtensions.cs). Por exemplo, as duas chamadas de log a seguir são funcionalmente equivalentes e produzem o mesmo log:

```csharp
public void LogDetails()
{
    var logMessage = "Details for log.";

    _logger.Log(LogLevel.Information, AppLogEvents.Details, logMessage);
    _logger.LogInformation(AppLogEvents.Details, logMessage);
}
```

`AppLogEvents.Details` é a ID do evento e é representada implicitamente por um <xref:System.Int32> valor constante. `AppLogEvents` é uma classe que expõe várias constantes de identificador nomeado e é exibida na seção [ID do evento de log](#log-event-id) .

O código a seguir cria os logs `Information` e `Warning`:

```csharp
public async Task<T> GetAsync<T>(string id)
{
    _logger.LogInformation(AppLogEvents.Read, "Reading value for {Id}", id);

    var result = await _repository.GetAsync(id);
    if (result is null)
    {
        _logger.LogWarning(AppLogEvents.ReadNotFound, "GetAsync({Id}) not found", id);
    }

    return result;
}
```

No código anterior, o primeiro `Log{LogLevel}` parâmetro, `AppLogEvents.Read` , é a [ID do evento de log](#log-event-id). O segundo parâmetro é um modelo de mensagem com espaços reservados para valores de argumento fornecidos pelos parâmetros de método restantes. Os parâmetros do método são explicados na seção de [modelo de mensagem](#log-message-template) mais adiante neste artigo.

Configure o nível de log apropriado e chame os `Log{LogLevel}` métodos corretos para controlar a quantidade de saída de log gravada em um meio de armazenamento específico. Por exemplo:

- Em produção:
  - O registro em log nos `Trace` `Information` níveis ou produz um alto volume de mensagens de log detalhadas. Para controlar os custos e não exceder os limites de armazenamento de dados, `Trace` as mensagens de log e de `Information` nível para um armazenamento de dados de alto volume e baixo custo. Considere limitar `Trace` e `Information` para categorias específicas.
  - O registro em log `Warning` por meio de `Critical` níveis deve produzir algumas mensagens de log.
    - Os custos e os limites de armazenamento geralmente não são uma preocupação.
    - Alguns logs permitem mais flexibilidade em opções de armazenamento de dados.
- Em desenvolvimento:
  - Defina como `Warning`.
  - Adicionar `Trace` ou `Information` mensagens ao solucionar problemas. Para limitar a saída, defina `Trace` ou `Information` apenas para as categorias em investigação.

Os seguintes conjuntos JSON `Logging:Console:LogLevel:Microsoft:Information` :

:::code language="json" source="snippets/configuration/worker-service/appsettings.MSFT.json":::

## <a name="log-event-id"></a>ID de evento de log

Cada log pode especificar um *identificador de evento*, o <xref:Microsoft.Extensions.Logging.EventId> é uma estrutura com `Id` `Name` as propriedades ReadOnly opcionais. O código-fonte de exemplo usa a `AppLogEvents` classe para definir IDs de evento:

```csharp
internal static class AppLogEvents
{
    internal const int Create = 1000;
    internal const int Read = 1001;
    internal const int Update = 1002;
    internal const int Delete = 1003;

    internal const int Details = 3000;
    internal const int Error = 3001;

    internal const int ReadNotFound = 4000;
    internal const int UpdateNotFound = 4001;

    // ...
}
```

Uma ID de evento associa um conjunto de eventos. Por exemplo, todos os logs relacionados à leitura de valores de um repositório podem ser `1001` .

O provedor de registro em log pode registrar a ID do evento em um campo de ID, na mensagem de registro ou não. O provedor de Depuração não mostra IDs de eventos. O provedor de console mostra IDs de evento entre colchetes após a categoria:

```console
info: Example.DefaultService.GetAsync[1001]
      Reading value for a1b2c3
warn: Example.DefaultService.GetAsync[4000]
      GetAsync(a1b2c3) not found
```

Alguns provedores de log armazenam a ID do evento em um campo, que permite filtrar a ID.

## <a name="log-message-template"></a>Modelo de mensagem de log

Cada API de log usa um modelo de mensagem. O modelo de mensagem pode conter espaços reservados para os quais são fornecidos argumentos. Use nomes para os espaços reservados, não números. A ordem dos espaços reservados e não de seus nomes, determina quais parâmetros serão usados para fornecer seus valores. No código a seguir, os nomes de parâmetro estão fora de sequência no modelo de mensagem:

```csharp
string p1 = "param1";
string p2 = "param2";
_logger.LogInformation("Parameter values: {p2}, {p1}", p1, p2);
```

O código anterior cria uma mensagem de log com os valores de parâmetro em sequência:

```text
Parameter values: param1, param2
```

Essa abordagem permite que os provedores de log implementem [logs semânticos ou estruturados](https://github.com/NLog/NLog/wiki/How-to-use-structured-logging). Os próprios argumentos são passados para o sistema de registro em log, não apenas o modelo de mensagem formatado. Isso permite que os provedores de log armazenem os valores de parâmetro como campos. Considere o seguinte método de agente:

```csharp
_logger.LogInformation("Getting item {Id} at {RunTime}", id, DateTime.Now);
```

Por exemplo, ao fazer logon no armazenamento de tabelas do Azure:

- Cada entidade de tabela do Azure pode ter `ID` `RunTime` Propriedades e.
- Tabelas com propriedades simplificam consultas em dados registrados. Por exemplo, uma consulta pode localizar todos os logs em um `RunTime` intervalo específico sem precisar analisar o tempo de saída da mensagem de texto.

## <a name="log-exceptions"></a>Registrar exceções em log

Os métodos de agente têm sobrecargas que usam um parâmetro de exceção:

```csharp
public void Test(string id)
{
    try
    {
        if (id == "none")
        {
            throw new Exception("Default Id detected.");
        }
    }
    catch (Exception ex)
    {
        _logger.LogWarning(
            AppLogEvents.Error, ex,
            "Failed to process iteration: {Id}", id)
    }
}
```

O log de exceções é específico do provedor.

### <a name="default-log-level"></a>Nível de log padrão

Se o nível de log padrão não for definido, o valor de nível de log padrão será `Information` .

Por exemplo, considere o seguinte aplicativo de serviço de trabalho:

- Criado com os modelos de trabalho do .NET.
- *appsettings.js* e *appsettings.Development.js* excluídos ou renomeados.

Com a configuração anterior, navegar até a privacidade ou home page produz muitas `Trace` `Debug` mensagens, e `Information`  com `Microsoft` no nome da categoria.

O código a seguir define o nível de log padrão quando o nível de log padrão não está definido na configuração:

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging => logging.SetMinimumLevel(LogLevel.Warning));
}
```

### <a name="filter-function"></a>Função Filter

Uma função de filtro é invocada para todos os provedores e categorias que não têm regras atribuídas a eles por configuração ou código:

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
                logging.AddFilter((provider, category, logLevel) =>
                {
                    return provider.Contains("ConsoleLoggerProvider")
                        && (category.Contains("Example") || category.Contains("Microsoft"))
                        && logLevel >= LogLevel.Information;
                }));
}
```

O código anterior exibe os logs do console quando a categoria contém `Example` ou `Microsoft` e o nível de log é `Information` ou superior.

## <a name="log-scopes"></a>Escopos de log

 Um *escopo* pode agrupar um conjunto de operações lógicas. Esse agrupamento pode ser usado para anexar os mesmos dados para cada log criado como parte de um conjunto. Por exemplo, todo log criado como parte do processamento de uma transação pode incluir a ID da transação.

Um escopo:

- É um <xref:System.IDisposable> tipo que é retornado pelo <xref:Microsoft.Extensions.Logging.ILogger.BeginScope%2A> método.
- Dura até ser Descartado.

Os seguintes provedores dão suporte a escopos:

- `Console`
- [AzureAppServicesFile e AzureAppServicesBlob](xref:Microsoft.Extensions.Logging.AzureAppServices.BatchingLoggerOptions.IncludeScopes)

Use um escopo por meio do encapsulamento de chamadas de agente em um bloco `using`:

```csharp
public async Task<T> GetAsync<T>(string id)
{
    T result;

    using (_logger.BeginScope("using block message"))
    {
        _logger.LogInformation(
            AppLogEvents.Read, "Reading value for {Id}", id);

        var result = await _repository.GetAsync(id);
        if (result is null)
        {
            _logger.LogWarning(
                AppLogEvents.ReadNotFound, "GetAsync({Id}) not found", id);
        }
    }

    return result;
}
```

O JSON a seguir habilita os escopos para o provedor de console:

:::code language="json" source="snippets/configuration/worker-service/appsettings.IncludeScopes.json" highlight="9":::

O código a seguir habilita os escopos para o provedor de console:

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging((_, logging) =>
                logging.ClearProviders()
                    .AddConsole(options => options.IncludeScopes = true));
}
```

## <a name="non-host-console-app"></a>Aplicativo de console não host

O código de log para aplicativos sem um [host genérico](generic-host.md) difere na maneira como os [provedores são adicionados](logging-providers.md#built-in-logging-providers) e os [agentes são criados](#create-logs). Em um aplicativo de console não host, chame o método de extensão `Add{provider name}` do provedor ao criar um `LoggerFactory`:

```csharp
class Program
{
    static void Main(string[] args)
    {
        using var loggerFactory = LoggerFactory.Create(builder =>
        {
            builder
                .AddFilter("Microsoft", LogLevel.Warning)
                .AddFilter("System", LogLevel.Warning)
                .AddFilter("LoggingConsoleApp.Program", LogLevel.Debug)
                .AddConsole();
        });

        ILogger logger = loggerFactory.CreateLogger<Program>();
        logger.LogInformation("Example log message");
    }
}
```

O `loggerFactory` objeto é usado para criar uma <xref:Microsoft.Extensions.Logging.ILogger> instância.

## <a name="create-logs-in-main"></a>Criar logs no principal

O código a seguir faz logon `Main` obtendo uma `ILogger` instância de di após a criação do host:

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

class Program
{
    static Task Main(string[] args)
    {
        IHost host = Host.CreateDefaultBuilder(args).Build();

        var logger = host.Services.GetRequiredService<ILogger<Program>>();
        logger.LogInformation("Host created.");

        return host.RunAsync();
    }
}
```

### <a name="no-asynchronous-logger-methods"></a>Sem métodos de agente assíncronos

O registro em log deve ser tão rápido que não justifique o custo de desempenho de código assíncrono. Se um armazenamento de dados de log estiver lento, não grave-o diretamente. Considere gravar as mensagens de log em um repositório rápido inicialmente e, em seguida, movê-las para o armazenamento lento mais tarde. Por exemplo, ao fazer logon no SQL Server, não faça isso diretamente em um `Log` método, pois os `Log` métodos são síncronos. Em vez disso, adicione mensagens de log de forma síncrona a uma fila na memória e faça com que uma função de trabalho de plano de fundo efetue pull das mensagens para fora da fila para fazer o trabalho assíncrono de envio de dados por push para o SQL Server.

## <a name="change-log-levels-in-a-running-app"></a>Alterar os níveis de log em um aplicativo em execução

A API de registro em log não inclui um cenário para alterar os níveis de log enquanto um aplicativo está em execução. No entanto, alguns provedores de configuração são capazes de recarregar a configuração, o que exige um efeito imediato na configuração de log. Por exemplo, o [provedor de configuração de arquivo](configuration-providers.md#file-configuration-provider) recarrega a configuração de log por padrão. Se a configuração for alterada no código enquanto um aplicativo estiver em execução, o aplicativo poderá chamar [IConfigurationRoot. recarregar](xref:Microsoft.Extensions.Configuration.IConfigurationRoot.Reload%2A) para atualizar a configuração de log do aplicativo.

## <a name="nuget-packages"></a>Pacotes NuGet

As <xref:Microsoft.Extensions.Logging.ILogger%601> <xref:Microsoft.Extensions.Logging.ILoggerFactory> interfaces e implementações são incluídas no SDK do .NET Core. Eles também estão disponíveis nos seguintes pacotes NuGet:

- As interfaces estão em [Microsoft. Extensions. Logging. abstrações](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions).
- As implementações padrão estão em [Microsoft. Extensions. Logging](https://www.nuget.org/packages/microsoft.extensions.logging).

## <a name="apply-log-filter-rules-in-code"></a>Aplicar regras de filtro de log no código

A abordagem preferida para definir regras de filtro de log é usando a [configuração](configuration.md)do.

O exemplo a seguir mostra como registrar regras de filtro no código:

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
               logging.AddFilter("System", LogLevel.Debug)
                  .AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Information)
                  .AddFilter<ConsoleLoggerProvider>("Microsoft", LogLevel.Trace));
}
```

`logging.AddFilter("System", LogLevel.Debug)` Especifica a `System` categoria e o nível de log `Debug` . O filtro é aplicado a todos os provedores porque um provedor específico não foi configurado.

`AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Information)` especificado

- O `Debug` provedor de log.
- Nível `Information` de log e superior.
- Todas as categorias que começam com `"Microsoft"` .

## <a name="see-also"></a>Consulte também

- [Provedores de log no .NET](logging-providers.md)
- [Implementar um provedor de log personalizado no .NET](custom-logging-provider.md)
- [Formatação de log de console](console-log-formatter.md)
- [Registro em log de alto desempenho no .NET](high-performance-logging.md)
- Os bugs de log devem ser criados no repositório [github.com/dotnet/Extensions](https://github.com/dotnet/extensions/issues)
