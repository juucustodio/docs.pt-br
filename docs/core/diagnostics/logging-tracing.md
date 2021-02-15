---
title: Registro em log e rastreamento – .NET Core
description: Uma introdução ao rastreamento e registro em log do .NET Core.
ms.date: 10/12/2020
ms.openlocfilehash: a8c6d82ddb7bc3f8b4cc9eae9dd7aaf65732a0b8
ms.sourcegitcommit: 4df8e005c074ceb1f978f007b222fe253be2baf3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99548389"
---
# <a name="net-core-logging-and-tracing"></a>Log e rastreamento do .NET Core

O registro em log e o rastreamento são, na verdade, dois nomes para a mesma técnica. A técnica simples foi usada desde os primórdios dos computadores. Ele simplesmente envolve a instrumentação de um aplicativo para gravar a saída a ser consumida posteriormente.

## <a name="reasons-to-use-logging-and-tracing"></a>Motivos para usar o log e o rastreamento

Essa técnica simples é surpreendentemente poderosa. Ele pode ser usado em situações em que um depurador falha:

- Problemas que ocorrem por longos períodos podem ser difíceis de depurar com um depurador tradicional. Os logs permitem uma análise detalhada post mortem, abrangendo longos períodos. Por outro lado, os depuradores são limitados a análises em tempo real.
- Aplicativos distribuídos e com multithread costumam ser difíceis de depurar.  A anexação de um depurador tende a modificar comportamentos. Logs detalhados podem ser analisados conforme necessário para entender sistemas complexos.
- Problemas em aplicativos distribuídos podem surgir de uma interação complexa entre vários componentes, e talvez não seja plausível conectar um depurador a todas as partes do sistema.
- Muitos serviços não devem ser interrompidos. A anexação de um depurador geralmente causa falhas de tempo limite.
- Os problemas nem sempre são previstos. O registro em log e o rastreamento são projetados para baixa sobrecarga, de modo que os programas possam ser gravados caso ocorra um problema.

## <a name="net-core-apis"></a>APIs do .NET Core

### <a name="print-style-apis"></a>APIs de estilo de impressão

As <xref:System.Console?displayProperty=nameWithType> <xref:System.Diagnostics.Trace?displayProperty=nameWithType> classes, e <xref:System.Diagnostics.Debug?displayProperty=nameWithType> fornecem, cada uma, APIs semelhantes de estilo de impressão conveniente para o registro em log.

A escolha da API de estilo de impressão a ser usada cabe a você. As principais diferenças são:

- <xref:System.Console?displayProperty=nameWithType>
  - Está sempre habilitado e sempre grava no console.
  - Útil para informações que seu cliente talvez precise ver na versão.
  - Por ser a abordagem mais simples, costuma ser usado para a depuração temporária ad hoc. Geralmente, esse código de depuração nunca é submetido a check-in no controle do código-fonte.
- <xref:System.Diagnostics.Trace?displayProperty=nameWithType>
  - Habilitada somente quando `TRACE` é definida pela adição `#define TRACE` à sua fonte ou à especificação da opção `/d:TRACE` durante a compilação.
  - Grava em anexado <xref:System.Diagnostics.Trace.Listeners> , por padrão, o <xref:System.Diagnostics.DefaultTraceListener> .
  - Use essa API ao criar logs que serão habilitados na maioria dos builds.
- <xref:System.Diagnostics.Debug?displayProperty=nameWithType>
  - Habilitada somente quando `DEBUG` é definida pela adição `#define DEBUG` à sua fonte ou à especificação da opção `/d:DEBUG` durante a compilação.
  - Grava em um depurador anexado.
  - Em `*nix` gravações em stderr, se `COMPlus_DebugWriteToStdErr` estiver definido.
  - Use essa API ao criar logs que serão habilitados apenas nos builds de depuração.

### <a name="logging-events"></a>Eventos de log

As APIs a seguir são mais orientadas a eventos. Em vez de registrar cadeias de caracteres simples, eles registram objetos de evento.

- <xref:System.Diagnostics.Tracing.EventSource?displayProperty=nameWithType>
  - EventSource é a principal API de rastreamento do .NET Core raiz.
  - Disponível em todas as versões de .NET Standard.
  - Permite apenas rastrear objetos serializáveis.
  - Pode ser consumido em processo por meio de todas as instâncias de [EventListener](xref:System.Diagnostics.Tracing.EventListener) configuradas para consumir a EventSource.
  - Pode ser consumido fora do processo por meio de:
    - [EventPipe do .NET Core](./eventpipe.md) em todas as plataformas
    - [ETW (Rastreamento de Eventos para Windows)](/windows/win32/etw/event-tracing-portal)
    - [Estrutura de rastreamento do LTTng para Linux](https://lttng.org/)
      - Walkthrough: [coletar um rastreamento de LTTng usando PerfCollect](trace-perfcollect-lttng.md).

- <xref:System.Diagnostics.DiagnosticSource?displayProperty=nameWithType>
  - Incluído no .NET Core e como um [pacote NuGet](https://www.nuget.org/packages/System.Diagnostics.DiagnosticSource) para .NET Framework.
  - Permite o rastreamento em processo de objetos não serializáveis.
  - Inclui uma ponte para permitir que os campos selecionados de objetos registrados sejam gravados em um <xref:System.Diagnostics.Tracing.EventSource> .

- <xref:System.Diagnostics.Activity?displayProperty=nameWithType>
  - Fornece uma maneira definitiva de identificar mensagens de log resultantes de uma atividade ou transação específica. Esse objeto pode ser usado para correlacionar logs entre diferentes serviços.

- <xref:System.Diagnostics.EventLog?displayProperty=nameWithType>
  - Somente Windows.
  - Grava mensagens no log de eventos do Windows.
  - Os administradores do sistema esperam que as mensagens de erro fatais do aplicativo apareçam no log de eventos do Windows.

## <a name="distributed-tracing"></a>Rastreamento distribuído

O [rastreamento distribuído](./distributed-tracing.md) é a maneira de publicar e observar os dados de rastreamento em um sistema distribuído.

## <a name="ilogger-and-logging-frameworks"></a>ILogger e estruturas de registro em log

As APIs de nível baixo podem não ser a escolha certa para suas necessidades de registro em log. Talvez você queira considerar uma estrutura de registro em log.

A <xref:Microsoft.Extensions.Logging.ILogger> interface foi usada para criar uma interface de log comum em que os agentes podem ser inseridos por meio da injeção de dependência.

Por exemplo, para permitir que você faça a melhor escolha para o seu aplicativo, o .NET oferece suporte para uma seleção de estruturas internas e de terceiros:

- [Provedores de log internos do .NET](../extensions/logging-providers.md#built-in-logging-providers)
- [Provedores de log de terceiros do .NET](../extensions/logging-providers.md#third-party-logging-providers)

## <a name="logging-related-references"></a>Referências relacionadas ao log

- [Como: compilar condicionalmente com Trace e Debug](../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)

- [Como: adicionar instruções de rastreamento ao código de um aplicativo](../../framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)

- O [registro em log no .net](../extensions/logging.md) fornece uma visão geral das técnicas de log que ele suporta.

- A [interpolação de cadeia de caracteres C#](../../csharp/language-reference/tokens/interpolated.md) pode simplificar o código de registro

- [Lista de eventos do provedor de tempo de execução](../../fundamentals/diagnostics/runtime-events.md)

- [Provedores de eventos bem conhecidos no .NET](well-known-event-providers.md)

- A <xref:System.Exception.Message?displayProperty=nameWithType> propriedade é útil para registrar exceções.

- A <xref:System.Diagnostics.StackTrace?displayProperty=nameWithType> classe pode ser útil para fornecer informações de pilha em seus logs.

## <a name="performance-considerations"></a>Considerações sobre o desempenho

A formatação da cadeia de caracteres pode levar tempo de processamento de CPU perceptível.

Em aplicativos de desempenho crítico, é recomendável que você:

- Evite muitos registros em log quando ninguém estiver ouvindo. Evite construir mensagens de registro em log dispendiosas verificando se o log está habilitado primeiro.
- Registre apenas o que é útil.
- Adie a formatação sofisticada para o estágio de análise.
