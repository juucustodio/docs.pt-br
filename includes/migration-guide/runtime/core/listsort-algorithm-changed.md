---
ms.openlocfilehash: 09bd2c6312493f8b6369d05d8f1c4e88e4c05ece
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497879"
---
### <a name="listsort-algorithm-changed"></a>O algoritmo List.Sort foi alterado

#### <a name="details"></a>Detalhes

A partir do .NET Framework 4.5, o algoritmo de classificação de <xref:System.Collections.Generic.List%601?displayProperty=fullName> foi alterado (para ser uma classificação introspectiva em vez de uma classificação rápida). A classificação de <xref:System.Collections.Generic.List%601?displayProperty=fullName> nunca foi estável, mas essa alteração pode fazer com que cenários diferentes sejam classificados de maneiras instáveis. Isso significa apenas que itens equivalentes podem ser classificados em ordens diferentes em chamadas posteriores da API.

#### <a name="suggestion"></a>Sugestão

Como o algoritmo de classificação antigo também era instável (embora de maneiras ligeiramente diferentes), não deve haver nenhum código que dependa de itens equivalentes sempre serem classificados em uma ordem específica. Se houver casos de códigos que dependem disso e que tinham sorte com o comportamento antigo, esses códigos deverão ser atualizados para usar um comparador que classifique de forma determinista os itens na ordem desejada.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Transparente|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Collections.Generic.List%601.Sort?displayProperty=nameWithType>
- <xref:System.Collections.Generic.List%601.Sort(System.Collections.Generic.IComparer{%600})?displayProperty=nameWithType>
- <xref:System.Collections.Generic.List%601.Sort(System.Comparison{%600})?displayProperty=nameWithType>
- <xref:System.Collections.Generic.List%601.Sort(System.Int32,System.Int32,System.Collections.Generic.IComparer{%600})?displayProperty=nameWithType>

<!--

#### Affected APIs

- ``M:System.Collections.Generic.List`1.Sort``
- ``M:System.Collections.Generic.List`1.Sort(System.Collections.Generic.IComparer{`0})``
- ``M:System.Collections.Generic.List`1.Sort(System.Comparison{`0})``
- ``M:System.Collections.Generic.List`1.Sort(System.Int32,System.Int32,System.Collections.Generic.IComparer{`0})``

-->
