---
ms.openlocfilehash: a84d72813a46d6bb39f4710b35d2c9dc859e30ef
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497250"
---
### <a name="pageloadcomplete-event-no-longer-causes-systemwebuiwebcontrolsentitydatasource-control-to-invoke-data-binding"></a>O evento Page.LoadComplete não faz mais com que o controle System.Web.UI.WebControls.EntityDataSource invoque a associação de dados

#### <a name="details"></a>Detalhes

O evento <xref:System.Web.UI.Page.LoadComplete> não faz mais com que o controle <xref:System.Web.UI.WebControls.EntityDataSource?displayProperty=fullName> chame a associação de dados para alterações par criar/atualizar/excluir parâmetros. Essa alteração elimina um processamento irrelevante para o banco de dados, impede que os valores dos controles sejam redefinidos e gera um comportamento consistente com outros controles de dados, como <xref:System.Web.UI.WebControls.SqlDataSource?displayProperty=fullName> e <xref:System.Web.UI.WebControls.ObjectDataSource?displayProperty=fullName>. Essa alteração gera um comportamento diferente em um evento improvável no qual os aplicativos dependam da associação de dados no evento <xref:System.Web.UI.Page.LoadComplete>.

#### <a name="suggestion"></a>Sugestão

Se houver necessidade de vinculação de dados, invoque manualmente a associação de dados em um evento que seja anterior no post-back.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
