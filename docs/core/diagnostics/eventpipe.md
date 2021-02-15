---
title: Visão geral do EventPipe
description: Saiba mais sobre o EventPipe e como usá-lo para rastrear seus aplicativos .NET para diagnosticar problemas de desempenho.
ms.date: 11/09/2020
ms.topic: overview
ms.openlocfilehash: 00378c4f409b307afa9183e40de6078cdafd3ae7
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94820612"
---
# <a name="eventpipe"></a>EventPipe

EventPipe é um componente de tempo de execução que pode ser usado para coletar dados de rastreamento, semelhante ao ETW ou ao LTTng. O objetivo do EventPipe é permitir que os desenvolvedores do .NET rastreiem facilmente seus aplicativos .NET sem precisar contar com componentes nativos do sistema operacional específicos da plataforma, como o ETW ou o LTTng.

EventPipe é o mecanismo por trás de muitas das ferramentas de diagnóstico e pode ser usado para consumir eventos emitidos pelo tempo de execução, bem como eventos personalizados escritos com [EventSource](xref:System.Diagnostics.Tracing.EventSource).

Este artigo é uma visão geral de alto nível do EventPipe que descreve quando e como usar o EventPipe e como configurá-lo para melhor atender às suas necessidades.

## <a name="eventpipe-basics"></a>Noções básicas do EventPipe

O EventPipe agrega eventos emitidos por componentes de tempo de execução, por exemplo, o compilador just-in-time ou o coletor de lixo e eventos gravados de instâncias de [EventSource](xref:System.Diagnostics.Tracing.EventSource) nas bibliotecas e no código do usuário.

Os eventos são serializados e podem ser gravados diretamente em um arquivo ou consumidos por meio de uma porta de diagnóstico a partir de um processo de saída. No Windows, as portas de diagnóstico são implementadas como `NamedPipe` s. Em plataformas não Windows, como Linux ou macOS, ele é implementado usando soquetes de domínio do UNIX. Para obter mais informações sobre a porta de diagnóstico e como interagir com ela por meio de seu protocolo de comunicação entre processos personalizado, consulte a [documentação do protocolo IPC do Diagnostics](https://github.com/dotnet/diagnostics/blob/master/documentation/design-docs/ipc-protocol.md).

Em seguida, o EventPipe grava os eventos serializados no `.nettrace` formato de arquivo, seja como um fluxo por meio de portas de diagnóstico ou diretamente para um arquivo. Para saber mais sobre o formato de serialização EventPipe, consulte a [documentação do formato EventPipe](https://github.com/microsoft/perfview/blob/master/src/TraceEvent/EventPipe/EventPipeFormat.md).

## <a name="eventpipe-vs-etwlttng"></a>EventPipe vs. ETW/LTTng

O EventPipe faz parte do tempo de execução do .NET (CoreCLR) e foi projetado para funcionar da mesma forma em todas as plataformas com suporte do .NET Core. Isso permite que as ferramentas de rastreamento baseadas em EventPipe, como `dotnet-counters` , `dotnet-gcdump` e `dotnet-trace` , funcionem diretamente entre as plataformas.

No entanto, como EventPipe é um componente interno de tempo de execução, seu escopo é limitado ao código gerenciado e ao próprio tempo de execução. EventPipe não pode ser usado para acompanhar alguns eventos de nível inferior, como a resolução de uma pilha de código nativa ou a obtenção de vários eventos de kernel. Se você usar a interoperabilidade C/C++ em seu aplicativo ou desejar rastrear o tempo de execução em si (que é escrito em C++) ou desejar um diagnóstico mais profundo no comportamento do aplicativo que requer eventos de kernel (ou seja, eventos de alternância de contexto de thread nativo), você deve usar ETW ou [perf/LTTng](./trace-perfcollect-lttng.md).

Outra grande diferença entre EventPipe e ETW/LTTng é o requisito de privilégio de administrador/raiz. Para rastrear um aplicativo usando ETW ou LTTng, você precisa ser um administrador/raiz. Usando o EventPipe, você pode rastrear aplicativos, desde que o rastreador (por exemplo, `dotnet-trace` ) seja executado como o mesmo usuário que o usuário que iniciou o aplicativo.

A tabela a seguir é um resumo das diferenças entre EventPipe e ETW/LTTng.

|Recurso|EventPipe|ETW|LTTng|
|-------|---------|---|-----------|
|Plataforma cruzada|Sim|Não (somente no Windows)|Não (somente em distribuições do Linux com suporte)|
|Exigir privilégio de administrador/raiz|Não|Sim|Sim|
|Pode obter eventos de sistema operacional/kernel|Não|Sim|Sim|
|Pode resolver transchamadas nativas|Não|Sim|Sim|

## <a name="use-eventpipe-to-trace-your-net-application"></a>Usar o EventPipe para rastrear seu aplicativo .NET

Você pode usar o EventPipe para rastrear seu aplicativo .NET de várias maneiras:

* Use uma das [ferramentas de diagnóstico](#tools-that-use-eventpipe) criadas com base no EventPipe.

* Use a biblioteca [Microsoft. Diagnostics. NetCore. cliente](https://github.com/dotnet/diagnostics/blob/master/documentation/diagnostics-client-library-instructions.md) para escrever sua própria ferramenta para configurar e iniciar as sessões do EventPipe por conta própria.

* Use [variáveis de ambiente](#trace-using-environment-variables) para iniciar o EventPipe.

Depois de produzir um `nettrace` arquivo que contém seus eventos do EventPipe, você pode exibir o arquivo no [`PerfView`](https://github.com/Microsoft/perfview#perfview-overview) ou no Visual Studio. Em plataformas não Windows, você pode converter o `nettrace` arquivo em um `speedscope` formato de `Chromium` rastreamento ou usando o [`dotnet-trace convert`](./dotnet-trace.md#dotnet-trace-convert) comando e exibi-lo com o [`speedscope`](https://www.speedscope.app/) ou o Chrome devtools.

Você também pode analisar rastreamentos de EventPipe programaticamente com [TraceEvent](https://github.com/Microsoft/perfview/blob/master/documentation/TraceEvent/TraceEventLibrary.md).

### <a name="tools-that-use-eventpipe"></a>Ferramentas que usam EventPipe

Essa é a maneira mais fácil de usar o EventPipe para rastrear seu aplicativo. Para saber mais sobre como usar cada uma dessas ferramentas, consulte a documentação de cada ferramenta.

* [dotnet-os contadores](./dotnet-counters.md) permitem monitorar e coletar várias métricas emitidas pelo tempo de execução do .net e pelas bibliotecas principais, bem como métricas personalizadas que você pode escrever.

* [dotnet-gcdump](./dotnet-gcdump.md) permite coletar despejos de heap de GC de processos ao vivo para analisar o heap gerenciado de um aplicativo.

* [dotnet-Trace](./dotnet-trace.md) permite que você colete rastreamentos de aplicativos para analisar o desempenho.

## <a name="trace-using-environment-variables"></a>Rastrear usando variáveis de ambiente

O mecanismo preferencial para usar EventPipe é usar `dotnet-trace` ou a `Microsoft.Diagnostics.NETCore.Client` biblioteca.

No entanto, você pode usar as seguintes variáveis de ambiente para configurar uma sessão EventPipe em um aplicativo e fazer com que ela grave o rastreamento diretamente em um arquivo. Para interromper o rastreamento, saia do aplicativo.

* `COMPlus_EnableEventPipe`: Defina isso como `1` para iniciar uma sessão EventPipe que grava diretamente em um arquivo. O valor padrão é `0`.

* `COMPlus_EventPipeOutputPath`: O caminho para o arquivo de rastreamento EventPipe de saída quando ele é configurado para ser executado via `COMPlus_EnableEventPipe` . O valor padrão é `trace.nettrace` , que será criado no mesmo diretório do qual o aplicativo está sendo executado.

* `COMPlus_CircularBufferMB`: O tamanho do buffer interno usado pelo EventPipe quando ele é configurado para ser executado via `COMPlus_EnableEventPipe` .

* `COMPlus_EventPipeConfig`: Define a configuração de sessão EventPipe ao iniciar uma sessão EventPipe com `COMPlus_EnableEventPipe` .

  A sintaxe dela é a seguinte:

  `<provider>:<keyword>:<level>`

  Você também pode especificar vários provedores concatenando-os com uma vírgula:

  `<provider1>:<keyword1>:<level1>,<provider2>:<keyword2>:<level2>`

  Se essa variável de ambiente não estiver definida, mas o EventPipe estiver habilitado pelo `COMPlus_EnableEventPipe` , ele iniciará o rastreamento habilitando os provedores a seguir com as seguintes palavras-chave e níveis:

  - `Microsoft-Windows-DotNETRuntime:4c14fccbd:5`
  - `Microsoft-Windows-DotNETRuntimePrivate:4002000b:5`
  - `Microsoft-DotNETCore-SampleProfiler:0:5`
