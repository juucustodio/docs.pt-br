---
ms.openlocfilehash: 4d210eeedd2f228017634d29f11554deb6ed8079
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497621"
---
### <a name="gridviews-with-allowcustompaging-set-to-true-may-fire-the-pageindexchanging-event-when-leaving-the-final-page-of-the-view"></a>GridViews com AllowCustomPaging definido como verdadeiro pode acionar o evento PageIndexChanging ao deixar a página final do modo de exibição

#### <a name="details"></a>Detalhes

Um bug no .NET Framework 4.5 faz com que <xref:System.Web.UI.WebControls.GridView.PageIndexChanging?displayProperty=fullName>, às vezes, não seja acionado para <xref:System.Web.UI.WebControls.GridView?displayProperty=fullName>s com <xref:System.Web.UI.WebControls.GridView.AllowCustomPaging?displayProperty=fullName> habilitado.

#### <a name="suggestion"></a>Sugestão

Esse problema foi corrigido no .NET Framework 4.6 e pode ser resolvido com o upgrade para essa versão do .NET Framework. Como solução alternativa, o aplicativo pode fazer um BindGrid explícito em qualquer <code>Page_Load</code> que respeite essas condições (o <xref:System.Web.UI.WebControls.GridView?displayProperty=fullName> está na última página e Last<xref:System.Web.UI.WebControls.GridView.PageSize?displayProperty=fullName> é diferente de <xref:System.Web.UI.WebControls.GridView.PageSize?displayProperty=fullName>). Como alternativa, o aplicativo pode ser modificado para permitir a paginação (em vez da paginação personalizada), uma vez que esse cenário não demonstra o problema.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Web.UI.WebControls.GridView.AllowCustomPaging?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.Web.UI.WebControls.GridView.AllowCustomPaging`

-->
