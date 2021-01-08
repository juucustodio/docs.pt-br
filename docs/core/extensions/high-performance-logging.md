---
title: Registro em log de alto desempenho no .NET
author: IEvangelist
description: Saiba como usar o LoggerMessage para criar representantes que podem ser armazenados em cache e exigem menos alocações de objeto para cenários de registro em log de alto desempenho.
ms.author: dapine
ms.date: 01/04/2021
ms.openlocfilehash: 0031ff7a9f70cb0cf724fdf6dfa4fbe0a44af7c1
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025440"
---
# <a name="high-performance-logging-in-net"></a>Registro em log de alto desempenho no .NET

A <xref:Microsoft.Extensions.Logging.LoggerMessage> classe expõe a funcionalidade para criar delegados em cache que exigem menos alocações de objeto e menor sobrecarga computacional em comparação com os [métodos de extensão do agente](xref:Microsoft.Extensions.Logging.LoggerExtensions), como <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation%2A> e <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogDebug%2A> . Para cenários de registro em log de alto desempenho, use o padrão <xref:Microsoft.Extensions.Logging.LoggerMessage>.

<xref:Microsoft.Extensions.Logging.LoggerMessage> fornece as seguintes vantagens de desempenho em relação aos métodos de extensão do Agente:

- Métodos de extensão do agente exigem tipos de valor de conversão boxing, como `int`, em `object`. O padrão <xref:Microsoft.Extensions.Logging.LoggerMessage> evita a conversão boxing usando campos <xref:System.Action> estáticos e métodos de extensão com parâmetros fortemente tipados.
- Os métodos de extensão do agente precisam analisar o modelo de mensagem (cadeia de caracteres de formato nomeada) sempre que uma mensagem de log é gravada. <xref:Microsoft.Extensions.Logging.LoggerMessage> exige apenas a análise de um modelo uma vez quando a mensagem é definida.

O aplicativo de exemplo demonstra <xref:Microsoft.Extensions.Logging.LoggerMessage> recursos com um serviço de trabalho de processamento de fila de prioridade. O aplicativo processa itens de trabalho em ordem de prioridade. Conforme ocorrem essas operações, são geradas mensagens de log usando o padrão <xref:Microsoft.Extensions.Logging.LoggerMessage>.

## <a name="define-a-logger-message"></a>Definir uma mensagem de agente

Use [define (LogLevel, EventID, String)](xref:Microsoft.Extensions.Logging.LoggerMessage.Define%2A) para criar um <xref:System.Action> delegado para registrar uma mensagem. Sobrecargas de <xref:Microsoft.Extensions.Logging.LoggerMessage.Define%2A> permitem passar até seis parâmetros de tipo para uma cadeia de caracteres de formato nomeada (modelo).

A cadeia de caracteres fornecida para o método <xref:Microsoft.Extensions.Logging.LoggerMessage.Define%2A> é um modelo e não uma cadeia de caracteres interpolada. Os espaços reservados são preenchidos na ordem em que os tipos são especificados. Os nomes do espaço reservado no modelo devem ser descritivos e consistentes em todos os modelos. Eles servem como nomes de propriedade em dados de log estruturado. Recomendamos o uso da [formatação Pascal Case](../../standard/design-guidelines/capitalization-conventions.md) para nomes de espaço reservado. Por exemplo, `{Item}`, `{DateTime}`.

Cada mensagem de log é uma <xref:System.Action> mantida em um campo estático criado por [LoggerMessage.Define](xref:Microsoft.Extensions.Logging.LoggerMessage.Define%2A). Por exemplo, o aplicativo de exemplo cria um campo para descrever uma mensagem de log para o processamento de itens de trabalho:

:::code language="csharp" source="snippets/configuration/worker-service-options/Extensions/LoggerExtensions.cs" id="FailedProcessingField":::

Para a <xref:System.Action>, especifique:

- O nível de log.
- Um identificador de evento exclusivo (<xref:Microsoft.Extensions.Logging.EventId>) com o nome do método de extensão estático.
- O modelo de mensagem (cadeia de caracteres de formato nomeada).

À medida que os itens de trabalho são recolocados na fila para processamento, o aplicativo do serviço de trabalho define:

- O nível de log como <xref:Microsoft.Extensions.Logging.LogLevel.Critical?displayProperty=nameWithType>.
- A ID do evento como `13` com o nome do método `FailedToProcessWorkItem`.
- Modelo de mensagem (cadeia de caracteres de formato nomeada) como uma cadeia de caracteres.

:::code language="csharp" source="snippets/configuration/worker-service-options/Extensions/LoggerExtensions.cs" id="FailedProcessingAssignment":::

Repositórios de log estruturado podem usar o nome do evento quando recebem a ID do evento para enriquecer o log. Por exemplo, [Serilog](https://github.com/serilog/serilog-extensions-logging) usa o nome do evento.

A <xref:System.Action> é invocada por meio de um método de extensão fortemente tipado. O `PriorityItemProcessed` método registra uma mensagem toda vez que um item de trabalho está sendo processado. Enquanto, `FailedToProcessWorkItem` é chamado quando (e se) uma exceção ocorre:

:::code language="csharp" source="snippets/configuration/worker-service-options/Worker.cs" range="18-39" highlight="15-18":::

Inspecione a saída do console do aplicativo:

```console
crit: WorkerServiceOptions.Example.Worker[13]
      Epic failure processing item!
      System.Exception: Failed to verify communications.
         at WorkerServiceOptions.Example.Worker.ExecuteAsync(CancellationToken stoppingToken) in
         ..\Worker.cs:line 27
```

Para passar parâmetros para uma mensagem de log, defina até seis tipos ao criar o campo estático. O aplicativo de exemplo registra em log os detalhes do item de trabalho ao processar itens definindo um `WorkItem` tipo para o <xref:System.Action> campo:

:::code language="csharp" source="snippets/configuration/worker-service-options/Extensions/LoggerExtensions.cs" id="ProcessingItemField":::

O modelo de mensagem de log do delegado recebe seus valores de espaço reservado dos tipos fornecidos. O aplicativo de exemplo define um delegado para adicionar um item de trabalho em que o parâmetro item é um `WorkItem` :

:::code language="csharp" source="snippets/configuration/worker-service-options/Extensions/LoggerExtensions.cs" id="ProcessingItemAssignment":::

O método de extensão estático para registrar em log que um item de trabalho está sendo processado, `PriorityItemProcessed` , recebe o valor do argumento de item de trabalho e o passa para o <xref:System.Action> delegado:

:::code language="csharp" source="snippets/configuration/worker-service-options/Extensions/LoggerExtensions.cs" id="ProcessingItemMethod":::

No método do serviço de trabalho `ExecuteAsync` , `PriorityItemProcessed` é chamado para registrar a mensagem:

:::code language="csharp" source="snippets/configuration/worker-service-options/Worker.cs" range="18-39" highlight="12":::

Inspecione a saída do console do aplicativo:

```console
info: WorkerServiceOptions.Example.Worker[1]
      Processing priority item: Priority-Extreme (50db062a-9732-4418-936d-110549ad79e4): 'Verify communications'
```

## <a name="define-logger-message-scope"></a>Definir escopo de mensagem de agente

O método [DefineScope (String)](xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope%2A) cria um <xref:System.Func%601> delegado para definir um [escopo de log](logging.md#log-scopes). Sobrecargas de <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope%2A> permitem passar até três parâmetros de tipo para uma cadeia de caracteres de formato nomeada (modelo).

Como é o caso com o método <xref:Microsoft.Extensions.Logging.LoggerMessage.Define%2A>, a cadeia de caracteres fornecida ao método <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope%2A> é um modelo e não uma cadeia de caracteres interpolada. Os espaços reservados são preenchidos na ordem em que os tipos são especificados. Os nomes do espaço reservado no modelo devem ser descritivos e consistentes em todos os modelos. Eles servem como nomes de propriedade em dados de log estruturado. Recomendamos o uso da [formatação Pascal Case](../../standard/design-guidelines/capitalization-conventions.md) para nomes de espaço reservado. Por exemplo, `{Item}`, `{DateTime}`.

Defina um [escopo de log](logging.md#log-scopes) a ser aplicado a uma série de mensagens de log usando o método <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope%2A>. Habilite `IncludeScopes` na seção de agente do console de *appSettings.json*:

:::code language="json" source="snippets/configuration/worker-service-options/appsettings.json" highlight="3-5":::

Para criar um escopo de log, adicione um campo para conter um delegado <xref:System.Func%601> para o escopo. O aplicativo de exemplo cria um campo chamado `_processingWorkScope` (*Internal/LoggerExtensions.cs*):

:::code language="csharp" source="snippets/configuration/worker-service-options/Extensions/LoggerExtensions.cs" id="ProcessingWorkField":::

Use <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope%2A> para criar o delegado. Até três tipos podem ser especificados para uso como argumentos de modelo quando o delegado é invocado. O aplicativo de exemplo usa um modelo de mensagem que inclui a data e hora em que o processamento começou:

:::code language="csharp" source="snippets/configuration/worker-service-options/Extensions/LoggerExtensions.cs" id="ProcessingWorkAssignment":::

Forneça um método de extensão estático para a mensagem de log. Inclua os parâmetros de tipo para propriedades nomeadas exibidos no modelo de mensagem. O aplicativo de exemplo usa um `DateTime` para um carimbo de data/hora personalizado para registrar e retornar `_processingWorkScope` :

:::code language="csharp" source="snippets/configuration/worker-service-options/Extensions/LoggerExtensions.cs" id="ProcessingWorkMethod":::

O escopo encapsula as chamadas de extensão de log em um bloco [using](../../csharp/language-reference/keywords/using-statement.md):

:::code language="csharp" source="snippets/configuration/worker-service-options/Worker.cs" range="18-39" highlight="4":::

Inspecione as mensagens de log na saída do console do aplicativo. O resultado a seguir mostra a ordenação de prioridade de mensagens de log com a mensagem de escopo de log incluída:

```console
info: WorkerServiceOptions.Example.Worker[1]
      => Processing work, started at: 09/25/2020 14:30:45
      Processing priority item: Priority-Extreme (f5090ede-a337-4041-b914-f6bc0db5ae64): 'Verify communications'
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: ..\worker-service-options
info: WorkerServiceOptions.Example.Worker[1]
      => Processing work, started at: 09/25/2020 14:30:45
      Processing priority item: Priority-High (496d440f-2007-4391-b179-09d75ab52373): 'Validate collection'
info: WorkerServiceOptions.Example.Worker[1]
      => Processing work, started at: 09/25/2020 14:30:45
      Processing priority item: Priority-Medium (dea9e3f4-d7df-46d2-b7cd-5e0232eb98a5): 'Propagate selections'
info: WorkerServiceOptions.Example.Worker[1]
      => Processing work, started at: 09/25/2020 14:30:45
      Processing priority item: Priority-Medium (089d7f0d-da72-4b55-92fe-57b147838056): 'Enter pooling [contention]'
info: WorkerServiceOptions.Example.Worker[1]
      => Processing work, started at: 09/25/2020 14:30:45
      Processing priority item: Priority-Low (6e68c4be-089f-4450-9080-1ea63fcbb686): 'Health check network'
info: WorkerServiceOptions.Example.Worker[1]
      => Processing work, started at: 09/25/2020 14:30:45
      Processing priority item: Priority-Deferred (6f324134-6bb6-455f-81d4-553ab307c421): 'Ping weather service'
info: WorkerServiceOptions.Example.Worker[1]
      => Processing work, started at: 09/25/2020 14:30:45
      Processing priority item: Priority-Deferred (37bf736c-7a26-4a2a-9e56-e89bcf3b8f35): 'Set process state'
```

## <a name="see-also"></a>Veja também

- [Registro em log no .NET](logging.md)
