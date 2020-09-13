---
ms.openlocfilehash: fb339fb35cdcbba4f1c860fae9c17162c4cff596
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496703"
---
### <a name="sql_variant-data-uses-sql_variant-collation-rather-than-database-collation"></a>Os dados do Sql_variant usam a ordenação sql_variant em vez da ordenação de banco de dados

#### <a name="details"></a>Detalhes

Os dados do <code>sql_variant</code> usam a ordenação <code>sql_variant</code> em vez da ordenação de banco de dados.

#### <a name="suggestion"></a>Sugestão

Essa alteração aborda os possíveis dados corrompidos caso a ordenação do banco de dados seja diferente da ordenação <code>sql_variant</code>. Os aplicativos que dependem de dados corrompidos podem apresentar falhas.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Transparente|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
