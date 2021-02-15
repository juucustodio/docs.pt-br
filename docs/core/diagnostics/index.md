---
title: Visão geral das ferramentas de diagnóstico – .NET Core
description: Uma visão geral das ferramentas e das técnicas disponíveis para diagnosticar aplicativos .NET Core.
ms.date: 07/16/2020
ms.topic: overview
ms.openlocfilehash: ee79057e45700e17fdd37cc36288b790d64d7a09
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188472"
---
# <a name="what-diagnostic-tools-are-available-in-net-core"></a>Quais ferramentas de diagnóstico estão disponíveis no .NET Core?

O software nem sempre se comporta como esperado, mas o .NET Core tem ferramentas e APIs que ajudarão você a diagnosticar esses problemas de maneira rápida e eficaz.

Este artigo ajuda a identificar as diversas ferramentas de que você precisa.

## <a name="managed-debuggers"></a>Depuradores gerenciados

Os [depuradores gerenciados](managed-debuggers.md) permitem que você interaja com seu programa. Pausar, executar incrementalmente, examinar e retomar fornecem informações sobre o comportamento do seu código. Um depurador é a primeira opção para diagnosticar problemas funcionais que podem ser facilmente reproduzidos.

## <a name="logging-and-tracing"></a>Registro em log e rastreamento

O [registro em log e o rastreamento](logging-tracing.md) são técnicas relacionadas. Eles se referem ao código de instrumentação para criar arquivos de log. Os arquivos registram os detalhes do que um programa faz. Esses detalhes podem ser usados para diagnosticar os problemas mais complexos. Quando aliados aos carimbos de data/hora, essas técnicas também são valiosas para as investigações de desempenho.

## <a name="metrics"></a>Métricas

O [EventCounters](event-counters.md) permite que você grave métricas para identificar e monitorar problemas de desempenho. As métricas incorrem em uma sobrecarga de desempenho inferior em comparação com o rastreamento, tornando-a mais adequada para um monitoramento de desempenho Always on. O tempo de execução e as bibliotecas do .NET publicam vários [EventCounters bem conhecidos](available-counters.md) que você também pode monitorar.

## <a name="unit-testing"></a>Teste de unidade

O [teste de unidade](../testing/index.md) é um componente fundamental da integração e da implantação contínuas de software de alta qualidade. Os testes de unidade são projetados para fornecer um aviso antecipado quando você interrompe algo.

## <a name="dumps"></a>Despejos

Um [despejo](./dumps.md) é um arquivo que contém um instantâneo do processo no momento da criação. Eles podem ser úteis para examinar o estado do aplicativo para fins de depuração.

## <a name="symbols"></a>Símbolos

Os símbolos são um requisito fundamental para depuração e outras ferramentas de diagnóstico. O conteúdo dos arquivos de símbolo varia entre linguagens, compiladores e plataformas. Em um símbolo de nível muito alto, há um mapeamento entre o código-fonte e o binário produzido pelo compilador. Esses mapeamentos são usados para fornecer itens como informações de número de linha e nomes de suas variáveis locais em ferramentas de diagnóstico, como o [Visual Studio](/visualstudio/debugger/what-is-debugging) e o [Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging).  O link a seguir contém uma explicação detalhada dos [símbolos](/windows/win32/dxtecharts/debugging-with-symbols) para o Windows, embora muitos dos conceitos também se apliquem a outras plataformas. Os [símbolos portáteis do .net](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md) têm uma extensão de arquivo "PDB" semelhante ao Windows PDB, embora não sejam compatíveis com o formato PDB do Windows.

## <a name="collect-diagnostics-in-containers"></a>Coletar diagnósticos em contêineres

As mesmas ferramentas de diagnóstico usadas em ambientes Linux não-contêineres também podem ser usadas para [coletar diagnósticos em contêineres](diagnostics-in-containers.md). Há apenas algumas alterações de uso necessárias para garantir que as ferramentas funcionem em um contêiner do Docker.

## <a name="net-core-diagnostic-global-tools"></a>Ferramentas globais de diagnóstico do .NET Core

### <a name="dotnet-counters"></a>dotnet-counters

[dotnet-os contadores](dotnet-counters.md) são uma ferramenta de monitoramento de desempenho para a investigação de desempenho e monitoramento de integridade de primeiro nível. Ele observa os valores do contador de desempenho publicados por meio da <xref:System.Diagnostics.Tracing.EventCounter> API. Por exemplo, você pode monitorar rapidamente coisas como o uso da CPU ou a taxa de exceções que estão sendo geradas em seu aplicativo .NET Core.

### <a name="dotnet-dump"></a>dotnet-dump

A ferramenta [dotnet-dump](dotnet-dump.md) é uma maneira de coletar e analisar despejos do Windows e do Linux Core sem um depurador nativo.

### <a name="dotnet-gcdump"></a>dotnet-gcdump

A ferramenta [dotnet-gcdump](dotnet-gcdump.md) é uma maneira de coletar despejos de GC (coletor de lixo) de processos do .net em tempo real.

### <a name="dotnet-trace"></a>dotnet-trace

O .NET Core inclui o que é chamado de `EventPipe` por meio do qual os dados de diagnóstico são expostos. A ferramenta [dotnet-Trace](dotnet-trace.md) permite que você consuma dados de criação de perfil interessantes de seu aplicativo que podem ajudar em cenários em que você precisa ter a causa raiz dos aplicativos em execução lenta.

### <a name="dotnet-symbol"></a>dotnet-symbol

[dotnet-Symbol](dotnet-symbol.md) baixa arquivos (símbolos, DAC/DBI, arquivos de host, etc.) necessários para abrir um dump principal ou minidespejo. Use essa ferramenta se precisar de símbolos e módulos para depurar um arquivo de despejo capturado em um computador diferente.

### <a name="dotnet-sos"></a>dotnet-sos

[dotnet-SOS](dotnet-sos.md) instala a [extensão de depuração SOS](sos-debugging-extension.md) no Linux e MacOS (e no Windows se você estiver usando o [windbg/CDB](/windows-hardware/drivers/debugger/debugger-download-tools)).

### <a name="perfcollect"></a>PerfCollect

[PerfCollect](trace-perfcollect-lttng.md) é um script bash que você pode usar para coletar rastreamentos com `perf` e `LTTng` para uma análise de desempenho mais detalhada de aplicativos .net em execução em distribuições do Linux.

## <a name="net-core-diagnostics-tutorials"></a>Tutoriais de diagnóstico do .NET Core

### <a name="debug-a-memory-leak"></a>Depurar um vazamento de memória

[Tutorial: Depurar um vazamento de memória](debug-memory-leak.md) percorre a localização de um vazamento de memória. A ferramenta [dotnet-Counters](dotnet-counters.md) é usada para confirmar o vazamento e a ferramenta [dotnet-dump](dotnet-dump.md) é usada para diagnosticar o vazamento.

### <a name="debug-high-cpu-usage"></a>Depurar alto uso da CPU

[Tutorial: Depurar alto uso da CPU](debug-highcpu.md) orienta você na investigação de alto uso da CPU. Ele usa a ferramenta [dotnet-Counters](dotnet-counters.md) para confirmar o alto uso da CPU. Em seguida, ele orienta você pelo uso [do trace for performance Analysis Utility ( `dotnet-trace` ) ou do](dotnet-trace.md) Linux `perf` para coletar e exibir o perfil de uso da CPU.

### <a name="debug-deadlock"></a>Depurar deadlock

[Tutorial: debug deadlock](debug-deadlock.md) mostra como usar a ferramenta [dotnet-dump](dotnet-dump.md) para investigar threads e bloqueios.

### <a name="debug-a-stackoverflow"></a>Depurar um StackOverflow

[Tutorial: Depurar um StackOverflow](debug-stackoverflow.md) demonstra como depurar um <xref:System.StackOverflowException> no Linux.

### <a name="debug-linux-dumps"></a>Depurar despejos do Linux

[Depurar despejos do Linux](debug-linux-dumps.md) explica como coletar e analisar despejos no Linux.

### <a name="measure-performance-using-eventcounters"></a>Medir o desempenho usando o EventCounters

[Tutorial: medir o desempenho usando o EventCounters no .net](event-counter-perf.md) mostra como usar a <xref:System.Diagnostics.Tracing.EventCounter> API para medir o desempenho em seu aplicativo .net.
