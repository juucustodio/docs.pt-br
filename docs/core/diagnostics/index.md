---
title: Visão geral das ferramentas de diagnóstico – .NET Core
description: Uma visão geral das ferramentas e das técnicas disponíveis para diagnosticar aplicativos .NET Core.
ms.date: 07/16/2020
ms.topic: overview
ms.openlocfilehash: 568f237e131cde18dad7c87ddff2fdd3d4bc5b8b
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89597983"
---
# <a name="what-diagnostic-tools-are-available-in-net-core"></a>Quais ferramentas de diagnóstico estão disponíveis no .NET Core?

O software nem sempre se comporta como esperado, mas o .NET Core tem ferramentas e APIs que ajudarão você a diagnosticar esses problemas de maneira rápida e eficaz.

Este artigo ajuda a identificar as diversas ferramentas de que você precisa.

## <a name="managed-debuggers"></a>Depuradores gerenciados

Os [depuradores gerenciados](managed-debuggers.md) permitem que você interaja com seu programa. Pausar, executar incrementalmente, examinar e retomar fornecem informações sobre o comportamento do seu código. Um depurador é a primeira opção para diagnosticar problemas funcionais que podem ser facilmente reproduzidos.

## <a name="logging-and-tracing"></a>Registro em log e rastreamento

O [registro em log e o rastreamento](logging-tracing.md) são técnicas relacionadas. Eles se referem ao código de instrumentação para criar arquivos de log. Os arquivos registram os detalhes do que um programa faz. Esses detalhes podem ser usados para diagnosticar os problemas mais complexos. Quando aliados aos carimbos de data/hora, essas técnicas também são valiosas para as investigações de desempenho.

## <a name="unit-testing"></a>Teste de unidade

O [teste de unidade](../testing/index.md) é um componente fundamental da integração e da implantação contínuas de software de alta qualidade. Os testes de unidade são projetados para fornecer um aviso antecipado quando você interrompe algo.

## <a name="debug-linux-dumps"></a>Depurar despejos do Linux

[Depurar despejos do Linux](debug-linux-dumps.md) explica como coletar e analisar despejos no Linux.

## <a name="net-core-diagnostic-global-tools"></a>Ferramentas globais de diagnóstico do .NET Core

### <a name="dotnet-counters"></a>dotnet-counters

[dotnet-os contadores](dotnet-counters.md) são uma ferramenta de monitoramento de desempenho para a investigação de desempenho e monitoramento de integridade de primeiro nível. Ele observa os valores do contador de desempenho publicados por meio da <xref:System.Diagnostics.Tracing.EventCounter> API. Por exemplo, você pode monitorar rapidamente coisas como o uso da CPU ou a taxa de exceções que estão sendo geradas em seu aplicativo .NET Core.

### <a name="dotnet-dump"></a>dotnet-dump

A ferramenta [dotnet-dump](dotnet-dump.md) é uma maneira de coletar e analisar despejos do Windows e do Linux Core sem um depurador nativo.

### <a name="dotnet-gcdump"></a>dotnet-gcdump

A ferramenta [dotnet-gcdump](dotnet-gcdump.md) é uma maneira de coletar despejos de GC (coletor de lixo) de processos do .net em tempo real.

### <a name="dotnet-trace"></a>dotnet-trace

O .NET Core inclui o que é chamado de `EventPipe` por meio do qual os dados de diagnóstico são expostos. A ferramenta [dotnet-Trace](dotnet-trace.md) permite que você consuma dados de criação de perfil interessantes de seu aplicativo que podem ajudar em cenários em que você precisa ter a causa raiz dos aplicativos em execução lenta.

### <a name="dotnet-symbol"></a>dotnet-símbolo

[dotnet-Symbol](dotnet-symbol.md) baixa arquivos (símbolos, DAC/DBI, arquivos de host, etc.) necessários para abrir um dump principal ou minidespejo. Use essa ferramenta se precisar de símbolos e módulos para depurar um arquivo de despejo capturado em um computador diferente.

### <a name="dotnet-sos"></a>dotnet-SOS

[dotnet-SOS](dotnet-sos.md) é usado para instalar a [extensão de depuração SOS](https://docs.microsoft.com/dotnet/framework/tools/sos-dll-sos-debugging-extension) no Linux ou MacOS (ou no Windows, se estiver usando ferramentas de depuração mais antigas).

## <a name="net-core-diagnostics-tutorials"></a>Tutoriais de diagnóstico do .NET Core

### <a name="debug-a-memory-leak"></a>Depurar um vazamento de memória

[Tutorial: Depurar um vazamento de memória](debug-memory-leak.md) percorre a localização de um vazamento de memória. A ferramenta [dotnet-Counters](dotnet-counters.md) é usada para confirmar o vazamento e a ferramenta [dotnet-dump](dotnet-dump.md) é usada para diagnosticar o vazamento.

### <a name="debug-high-cpu-usage"></a>Depurar alto uso da CPU

[Tutorial: Depurar alto uso da CPU](debug-highcpu.md) orienta você na investigação de alto uso da CPU. Ele usa a ferramenta [dotnet-Counters](dotnet-counters.md) para confirmar o alto uso da CPU. Em seguida, ele orienta você pelo uso [do trace for performance Analysis Utility ( `dotnet-trace` ) ou do](dotnet-trace.md) Linux `perf` para coletar e exibir o perfil de uso da CPU.

### <a name="debug-deadlock"></a>Depurar deadlock

[Tutorial: debug deadlock](debug-deadlock.md) mostra como usar a ferramenta [dotnet-dump](dotnet-dump.md) para investigar threads e bloqueios.
