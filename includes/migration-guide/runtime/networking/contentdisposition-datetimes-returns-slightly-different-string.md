---
ms.openlocfilehash: eb5c032a020799fa19cc0a8cfaabb56e01417ff4
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497638"
---
### <a name="contentdisposition-datetimes-returns-slightly-different-string"></a>ContentDisposition DateTimes retorna cadeia de caracteres ligeiramente diferente

#### <a name="details"></a>Detalhes

As representações de cadeia de caracteres de <xref:System.Net.Mime.ContentDisposition?displayProperty=fullName> foram atualizadas, a partir da versão 4.6, para sempre representarem o componente de hora de um <xref:System.DateTime?displayProperty=fullName> com dois dígitos. Isso está em conformidade com a [RFC822](https://www.ietf.org/rfc/rfc0822.txt) e [RFC2822](https://www.ietf.org/rfc/rfc2822.txt). Isso faz com que <xref:System.Net.Mime.ContentDisposition.ToString> retorne uma cadeia de caracteres ligeiramente diferente na versão 4.6 em cenários em que um dos elementos de tempo da disposição era anterior a 10:00 AM. Observe que ContentDispositions, às vezes, são serializados por meio de conversão em cadeias de caracteres, de modo que quaisquer operações <xref:System.Net.Mime.ContentDisposition.ToString>, serialização ou chamadas GetHashCode devem ser revisadas.

#### <a name="suggestion"></a>Sugestão

Não espere que essas representações de cadeia de caracteres de ContentDispositions de diferentes versões do .NET Framework sejam corretamente comparadas umas com as outras. Converta as cadeias de caracteres de volta em ContentDispositions, se possível, antes de realizar uma comparação.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.6|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Net.Mime.ContentDisposition.ToString?displayProperty=nameWithType>
- <xref:System.Net.Mime.ContentDisposition.GetHashCode?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Net.Mime.ContentDisposition.ToString`
- `M:System.Net.Mime.ContentDisposition.GetHashCode`

-->
