---
ms.openlocfilehash: 9d0791f00db7d830fc5d327af30218a0bbfcb25f
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497725"
---
### <a name="change-in-behavior-for-taskwaitall-methods-with-time-out-arguments"></a>Mudança no comportamento de métodos Task.WaitAll com argumentos de tempo limite

#### <a name="details"></a>Detalhes

O comportamento de <xref:System.Threading.Tasks.Task.WaitAll%2A?displayProperty=nameWithType> ficou mais consistente no .NET Framework 4.5. No .NET Framework 4, esses métodos se comportavam de forma inconsistente. Quando o tempo limite expirou, se uma ou mais tarefas foram concluídas ou canceladas antes da chamada de método, o método lançou uma exceção <xref:System.AggregateException?displayProperty=fullName>. Quando o tempo limite expirava, se nenhuma tarefa tivesse sido concluída ou cancelada antes da chamada de método, mas uma ou mais tarefas tivessem entrado nesses estados após a chamada de método, o método retornava false.<br/><br/>No .NET Framework 4.5, essas sobrecargas de método agora retornam false se alguma tarefa ainda está em execução quando o intervalo de tempo limite expira e geram uma exceção <xref:System.AggregateException?displayProperty=fullName> somente se uma tarefa de entrada é cancelada (não importa se antes ou depois da chamada de método) e nenhuma outra tarefa ainda está em execução.

#### <a name="suggestion"></a>Sugestão

Se um <xref:System.AggregateException?displayProperty=fullName> era capturado como um meio de detectar uma tarefa cancelada antes da invocação da chamada de <xref:System.Threading.Tasks.Task.WaitAll%2A>, esse código deverá fazer a mesma detecção por meio da propriedade <xref:System.Threading.Tasks.Task.IsCanceled%2A> [por exemplo: .Any(t =&gt; t.IsCanceled)], porque o .NET Framework 4.6 acionará esse caso apenas se todas as tarefas esperadas forem concluídas antes do tempo limite.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.5|
|Tipo|Runtime

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.Int32)?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.Int32,System.Threading.CancellationToken)?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.TimeSpan)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.Int32)`
- `M:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.Int32,System.Threading.CancellationToken)`
- `M:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.TimeSpan)`

-->
