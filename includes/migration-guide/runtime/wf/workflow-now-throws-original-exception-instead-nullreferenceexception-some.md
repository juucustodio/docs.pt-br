---
ms.openlocfilehash: 61d5885c19e39b138090c1a98fa26348724893c5
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497261"
---
### <a name="workflow-now-throws-original-exception-instead-of-nullreferenceexception-in-some-cases"></a>Agora, o fluxo de trabalho gera a exceção original em vez de NullReferenceException em alguns casos

#### <a name="details"></a>Detalhes

No .NET Framework 4.6.2 e versões anteriores, quando o método Executar de uma atividade de fluxo de trabalho gera uma exceção com um valor <code>null</code> para a propriedade <xref:System.Exception.Message>, o runtime do fluxo de trabalho System.Activities gera <xref:System.NullReferenceException?displayProperty=fullName>, mascarando a exceção original. No .NET Framework 4.7, a exceção mascarada anteriormente é gerada.

#### <a name="suggestion"></a>Sugestão

Se o código depender do tratamento de <xref:System.NullReferenceException?displayProperty=fullName>, altere-o para capturar as exceções que possam ser geradas por meio das atividades personalizadas.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.7|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Activities.CodeActivity.Execute(System.Activities.CodeActivityContext)?displayProperty=nameWithType>
- <xref:System.Activities.AsyncCodeActivity.BeginExecute(System.Activities.AsyncCodeActivityContext,System.AsyncCallback,System.Object)?displayProperty=nameWithType>
- <xref:System.Activities.AsyncCodeActivity%601.BeginExecute(System.Activities.AsyncCodeActivityContext,System.AsyncCallback,System.Object)?displayProperty=nameWithType>
- <xref:System.Activities.WorkflowInvoker.Invoke?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Activities.CodeActivity.Execute(System.Activities.CodeActivityContext)`
- `M:System.Activities.AsyncCodeActivity.BeginExecute(System.Activities.AsyncCodeActivityContext,System.AsyncCallback,System.Object)`
- ``M:System.Activities.AsyncCodeActivity`1.BeginExecute(System.Activities.AsyncCodeActivityContext,System.AsyncCallback,System.Object)``
- `M:System.Activities.WorkflowInvoker.Invoke`

-->
