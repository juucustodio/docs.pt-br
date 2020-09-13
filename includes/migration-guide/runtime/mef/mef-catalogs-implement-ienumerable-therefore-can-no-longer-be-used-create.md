---
ms.openlocfilehash: 6f22d6211ec9238fd1c7786643ca95db02bfca64
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497568"
---
### <a name="mef-catalogs-implement-ienumerable-and-therefore-can-no-longer-be-used-to-create-a-serializer"></a>Os catálogos do MEF implementam IEnumerable e, portanto, não podem mais ser usados para criar um serializador

#### <a name="details"></a>Detalhes

A partir do .NET Framework 4.5, os catálogos do MEF implementam IEnumerable e, portanto, não podem mais ser usados para criar um serializador (objeto <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName>). Tentar serializar um catálogo de MEF gera uma exceção.

#### <a name="suggestion"></a>Sugestão

Não é mais possível usar o MEF para criar um serializador

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Principal|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
