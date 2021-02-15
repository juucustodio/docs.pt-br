---
title: Provedores de eventos bem conhecidos no .NET
description: Examine os provedores e eventos publicados pelo tempo de execução e pelas bibliotecas do .NET.
ms.topic: reference
ms.date: 12/21/2020
ms.openlocfilehash: 03d505f33e300b094958676bb768fb542d828aeb
ms.sourcegitcommit: c3093e9d106d8ca87cc86eef1f2ae4ecfb392118
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2020
ms.locfileid: "97738197"
---
# <a name="well-known-event-providers-in-net"></a>Provedores de eventos bem conhecidos no .NET

O tempo de execução e as bibliotecas do .NET gravam eventos de diagnóstico por meio de vários provedores de eventos diferentes. Dependendo das suas necessidades de diagnóstico, você pode escolher os provedores apropriados a serem habilitados. Este artigo descreve alguns dos provedores de eventos usados com mais frequência no tempo de execução e nas bibliotecas do .NET.

## <a name="coreclr"></a>CoreCLR

### <a name="microsoft-windows-dotnetruntime-provider"></a>Provedor "Microsoft-Windows-DotNETRuntime"

Esse provedor emite vários eventos do tempo de execução do .NET, incluindo GC, Loader, JIT, exceção e outros eventos. Leia mais sobre cada evento desse provedor na [lista de eventos do provedor de tempo de execução](../../fundamentals/diagnostics/runtime-events.md).

### <a name="microsoft-dotnetcore-sampleprofiler-provider"></a>Provedor "Microsoft-DotNETCore-SampleProfiler"

Este provedor é um provedor de eventos de tempo de execução .NET que é usado para amostragem de CPU para pilhas de chamadas gerenciadas. Quando habilitado, ele captura um instantâneo da pilha de chamadas gerenciada de cada thread a cada 10 milissegundos. Para habilitar essa captura, você deve especificar um <xref:System.Diagnostics.Tracing.EventLevel> `Informational` ou superior.

## <a name="framework-libraries"></a>Bibliotecas do Framework

### <a name="microsoft-extensions-dependencyinjection-provider"></a>Provedor "Microsoft-Extensions-DependencyInjection"

Este provedor registra informações de DependencyInjection. A tabela a seguir mostra os eventos registrados pelo `Microsoft-Extensions-DependencyInjection` provedor:

|Nome do evento|Nível|Descrição|
|----------|-----|-----------|
|`CallSiteBuilt`|Detalhado (5)|Um site de chamada foi criado.|
|`ServiceResolved`|Detalhado (5)|Um serviço foi resolvido.|
|`ExpressionTreeGenerated`|Detalhado (5)|Uma árvore de expressão foi gerada.|
|`DynamicMethodBuilt`|Detalhado (5)|Um <xref:System.Reflection.Emit.DynamicMethod> foi criado.|

### <a name="systembuffersarraypooleventsource-provider"></a>Provedor "System. buffers. ArrayPoolEventSource"

Esse provedor registra informações do ArrayPool. A tabela a seguir mostra os eventos registrados por `ArrayPoolEventSource` :

|Nome do evento|Nível|Descrição|
|----------|-----|-----------|
|`BufferRented`|Detalhado (5)|Um buffer foi alugado com êxito.|
|`BufferAllocated`|Informativo (4)|Um buffer é alocado pelo pool.|
|`BufferReturned`|Detalhado (5)|Um buffer é retornado para o pool.|
|`BufferTrimmed`|Informativo (4)|Tentativa de liberação de buffer devido a uma pressão de memória ou inatividade.|
|`BufferTrimPoll`|Informativo (4)|Está sendo feita uma verificação para reduzir os buffers.|

### <a name="systemnethttp-provider"></a>Provedor "System .net. http"

Esse provedor registra informações da pilha HTTP. A tabela a seguir mostra os eventos registrados pelo `System.Net.Http` provedor:

|Nome do evento|Nível|Descrição|
|----------|-----|-----------|
|RequestStart|Informativo (4)|Uma solicitação HTTP foi iniciada.|
|RequestStop|Informativo (4)|Uma solicitação HTTP foi concluída.|
|RequestFailed|Erro (2)|Falha em uma solicitação HTTP.|
|ConnectionEstablished|Informativo (4)|Uma conexão HTTP foi estabelecida.|
|ConnectionClosed|Informativo (4)|Uma conexão HTTP foi fechada.|
|RequestLeftQueue|Informativo (4)|Uma solicitação HTTP saiu da fila de solicitações.|
|RequestHeadersStart|Informativo (4)|Uma solicitação HTTP para o cabeçalho foi iniciada.|
|RequestHeaderStop|Informativo (4)|Uma solicitação HTTP para o cabeçalho foi concluída.|
|RequestContentStart|Informativo (4)|Uma solicitação HTTP de conteúdo foi iniciada.|
|RequestContentStop|Informativo (4)|Uma solicitação HTTP de conteúdo foi concluída.|
|ResponseHeadersStart|Informativo (4)|Uma resposta HTTP para o cabeçalho foi iniciada.|
|ResponseHeaderStop|Informativo (4)|Uma resposta HTTP para o cabeçalho foi concluída.|
|ResponseContentStart|Informativo (4)|Uma resposta HTTP para o conteúdo foi iniciada.|
|ResponseContentStop|Informativo (4)|Uma resposta HTTP para o conteúdo foi concluída.|

### <a name="systemnetnameresolution-provider"></a>Provedor "System .net. NameResolution"

Este provedor registra informações relacionadas à resolução de nomes de domínio. A tabela a seguir mostra os eventos registrados por `System.Net.NameResolution` :

|Nome do evento|Nível|Descrição|
|----------|-----|-----------|
|`ResolutionStart`|Informativo (4)|Uma resolução de nome de domínio foi iniciada.|
|`ResolutionStop`|Informativo (4)|Uma resolução de nome de domínio foi concluída.|
|`ResolutionFailed`|Informativo (4)|Falha na resolução de nome de domínio.|

### <a name="systemnetsockets-provider"></a>Provedor "System .net. Sockets"

Este provedor registra informações de <xref:System.Net.Sockets.Socket> . A tabela a seguir mostra os eventos registrados pelo `System.Net.Sockets` provedor:

|Nome do evento|Nível|Descrição|
|----------|-----|-----------|
|`ConnectStart`|Informativo (4)|Foi iniciada uma tentativa de iniciar uma conexão de soquete.|
|`ConnectStop`|Informativo (4)|Foi concluída uma tentativa de iniciar uma conexão de soquete.|
|`ConnectFailed`|Informativo (4)|Falha ao tentar iniciar uma conexão de soquete.|
|`AcceptStart`|Informativo (4)|Foi iniciada uma tentativa de aceitar uma conexão de soquete.|
|`AcceptStop`|Informativo (4)|Foi concluída uma tentativa de aceitar uma conexão de soquete.|
|`AcceptFailed`|Informativo (4)|Falha ao tentar aceitar uma conexão de soquete.|

### <a name="systemthreadingtaskstpleventsource-provider"></a>Provedor "System. Threading. Tasks. TplEventSource"

Esse provedor registra informações sobre a [biblioteca de tarefas paralelas](../../standard/parallel-programming/task-parallel-library-tpl.md), como eventos do Agendador de tarefas. A tabela a seguir mostra os eventos registrados por `TplEventSource` :

|Nome do evento|Palavra-chave|Nível|Descrição|
|----------|-------|-----|-----------|
|`TaskScheduled`|`TaskTransfer`(`0x1`)<br /><br />`Tasks`(`0x2`)|Informativo (4)|Um <xref:System.Threading.Tasks.Task> é enfileirado para o Agendador de tarefas.|
|`TaskStarted`|`Tasks`(`0x2`)|Informativo (4)|Um <xref:System.Threading.Tasks.Task> começou A ser executado.|
|`TaskCompleted`|`TaskStops`(`0x40`)|Informativo (4)|Um concluiu A <xref:System.Threading.Tasks.Task> execução.|
|`TaskWaitBegin`|`TaskTransfer`(`0x1`)<br /><br />`TaskWait`(`0x2`)|Informativo (4)|Acionado quando uma espera implícita ou explícita em uma <xref:System.Threading.Tasks.Task> conclusão é iniciada.|
|`TaskWaitEnd`|`Tasks`(`0x2`)|Detalhado (5)|Acionado quando a espera de uma <xref:System.Threading.Tasks.Task> conclusão retorna.|
|`TaskWaitContinuationStarted`|`Tasks`(`0x2`)|Detalhado (5)|Acionado quando o trabalho (método) associado a um `TaskWaitEnd` é iniciado.|
|`TaskWaitContinuationCompleted`|`TaskStops`(`0x40`)|Detalhado (5)|Acionado quando o trabalho (método) associado a um `TaskWaitEnd` é concluído.|
|`AwaitTaskContinuationScheduled`|`TaskTransfer`(`0x1`)<br /><br />`Tasks`(`0x2`)|Informativo (4)|Acionado quando a continuação assíncrona de um <xref:System.Threading.Tasks.Task> é agendada.|

## <a name="aspnet-core"></a>ASP.NET Core

O ASP.NET Core também fornece vários eventos para ajudá-lo a diagnosticar problemas na pilha ASP.NET Core.

Para saber mais sobre os eventos em ASP.NET Core e como consumi-los, consulte [Logging in .NET Core e ASP.NET Core](/aspnet/core/fundamentals/logging/).
