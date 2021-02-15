---
ms.openlocfilehash: 1f85b1ce95ca07329aff77af4ec894622e0818d1
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606593"
---
### <a name="workflow-30-types-are-obsolete"></a>Os tipos do WorkFlow 3.0 estão obsoletos

#### <a name="details"></a>Detalhes

As APIs (aquelas do namespace System.Workflow) do WWF (Windows Workflow Foundation) 3.0 agora estão obsoletas.

#### <a name="suggestion"></a>Sugestão

Agora devem ser usadas as novas APIs (em System.Activities) do WWF 4.0. Um exemplo de como usar as novas APIs pode ser encontrado [aqui](~/docs/framework/windows-workflow-foundation/how-to-update-the-definition-of-a-running-workflow-instance.md), e outras diretrizes estão disponíveis [aqui](/archive/blogs/workflowteam/wf3-types-marked-obsolete-in-net-4-5). Como alternativa, uma vez que as APIs do WWF 3.0 ainda têm suporte, elas poderão ser usadas, e o aviso de hora da compilação deve ser evitado suprimindo-o ou usando um compilador mais antigo.

| Name    | Valor       |
|:--------|:------------|
| Escopo   | Principal       |
| Versão | 4.5         |
| Tipo    | Redirecionando |
