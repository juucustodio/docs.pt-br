---
ms.openlocfilehash: 3c32d2e13447f8fd9aa6b185b5fc7e60f9e1bb61
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497610"
---
### <a name="support-special-relative-uri-notation-when-unicode-is-present"></a>Permitir notação de URI relativo especial quando o Unicode estiver presente

#### <a name="details"></a>Detalhes

<xref:System.Uri> não gerará mais um <xref:System.NullReferenceException> ao chamar <xref:System.Uri.TryCreate%2A> em determinados URIs relativos que contenham Unicode. A reprodução mais simples do <xref:System.NullReferenceException> está abaixo, com as duas instruções sendo equivalentes:<pre><code class="lang-csharp">bool success = Uri.TryCreate(&quot;http:%C3%A8&quot;, UriKind.RelativeOrAbsolute, out Uri href);&#13;&#10;bool success = Uri.TryCreate(&quot;http:&#232;&quot;, UriKind.RelativeOrAbsolute, out Uri href);&#13;&#10;</code></pre>Para reproduzir a <xref:System.NullReferenceException>, os itens a seguir precisam ser verdadeiros:<ul><li>O URI precisa ser especificado como relativo acrescentando 'http:' a ele e não inserindo '//' depois dele.</li><li>O URI precisa conter Unicode codificado por porcentagem ou símbolos não reservados.</li></ul>

#### <a name="suggestion"></a>Sugestão

Os usuários que dependem desse comportamento para não permitir URIs relativos precisam especificar <xref:System.UriKind.Absolute?displayProperty=nameWithType> durante a criação de um URI.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.7.2|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Uri.TryCreate(System.Uri,System.Uri,System.Uri@)?displayProperty=nameWithType>
- <xref:System.Uri.TryCreate(System.String,System.UriKind,System.Uri@)?displayProperty=nameWithType>
- <xref:System.Uri.TryCreate(System.Uri,System.String,System.Uri@)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Uri.TryCreate(System.Uri,System.Uri,System.Uri@)`
- `M:System.Uri.TryCreate(System.String,System.UriKind,System.Uri@)`
- `M:System.Uri.TryCreate(System.Uri,System.String,System.Uri@)`

-->
