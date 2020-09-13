---
ms.openlocfilehash: 61749f59f9379a6d18bb013b2612a07cb7822b3a
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496270"
---
### <a name="new-enum-values-in-wpfs-pagerangeselection"></a>Novos valores de enumeração em PageRangeSelection do WPF

#### <a name="details"></a>Detalhes

Os dois novos membros (<xref:System.Windows.Controls.PageRangeSelection.CurrentPage?displayProperty=fullName> e <xref:System.Windows.Controls.PageRangeSelection.SelectedPages?displayProperty=fullName>) foram adicionados à enumeração <xref:System.Windows.Controls.PageRangeSelection?displayProperty=fullName>.

#### <a name="suggestion"></a>Sugestão

Na maioria das vezes, essas mudanças não afetarão o código do usuário. O código que depende de um número específico de elementos existentes nas chamadas <xref:System.Enum.GetNames(System.Type)> ou <xref:System.Enum.GetValues(System.Type)> no tipo <xref:System.Windows.Controls.PageRangeSelection?displayProperty=fullName> deve ser modificado.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.Controls.PageRangeSelection?displayProperty=nameWithType>

<!--

#### Affected APIs

- `T:System.Windows.Controls.PageRangeSelection`

-->
