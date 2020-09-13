---
ms.openlocfilehash: 58dbb54d42d89b450134758072e3133ae4e6b13d
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496241"
---
### <a name="systemthreadingtaskstask-no-longer-throw-objectdisposedexception-after-object-is-disposed"></a>System.Threading.Tasks.Task não gera mais ObjectDisposedException depois que o objeto é descartado

#### <a name="details"></a>Detalhes

Exceto por <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle>, os métodos <xref:System.Threading.Tasks.Task?displayProperty=fullName>não geram mais uma exceção <xref:System.ObjectDisposedException?displayProperty=fullName> após o objeto ser descartado. Essa alteração permite o uso de tarefas em cache. Por exemplo, um método pode retornar uma tarefa em cache para representar uma operação já concluída em vez de alocar uma nova tarefa. Isso era impossível nas versões anteriores do .NET Framework porque qualquer consumidor da tarefa poderia descartá-los, o que a tornava inutilizável.

#### <a name="suggestion"></a>Sugestão

Lembre-se de que os métodos Task podem não gerar mais <xref:System.ObjectDisposedException?displayProperty=fullName> nos casos em que o objeto é descartado. Se um aplicativo dependia dessa exceção para saber que uma tarefa foi descartada, ele deverá ser atualizado para verificar explicitamente o status da tarefa usando <xref:System.Threading.Tasks.Task.Status>.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
