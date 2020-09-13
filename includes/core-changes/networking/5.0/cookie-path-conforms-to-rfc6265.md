---
ms.openlocfilehash: 7140f6d4cac063088b3663ab98d292104218b542
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465501"
---
### <a name="cookie-path-handling-now-conforms-to-rfc-6265"></a>O tratamento de caminho de cookie agora está em conformidade com RFC 6265

Os algoritmos de tratamento de caminho definidos no [RFC 6265](https://tools.ietf.org/html/rfc6265) foram implementados para as <xref:System.Net.Cookie> <xref:System.Net.CookieContainer> classes e.

#### <a name="version-introduced"></a>Versão introduzida

5,0

#### <a name="change-description"></a>Descrição das alterações

- A <xref:System.Net.Cookie.Path> propriedade não é mais necessária para ser um prefixo do caminho da solicitação.
- O cálculo do valor padrão do <xref:System.Net.Cookie.Path> e dos algoritmos de correspondência de caminho foram implementados conforme definido na [seção 5.1.4](https://tools.ietf.org/html/rfc6265#section-5.1.4) do RFC 6265.

#### <a name="recommended-action"></a>Ação recomendada

Na maioria dos casos, você não precisará realizar nenhuma ação. No entanto, se o seu código depender da <xref:System.Net.Cookie.Path> validação, você precisará implementar a validação necessária em seu código. Se o seu código depender do cálculo do valor padrão para <xref:System.Net.Cookie.Path> , considere fornecer o <xref:System.Net.Cookie.Path> valor manualmente em vez de usar o valor padrão.

#### <a name="category"></a>Categoria

Rede

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Net.Cookie?displayProperty=fullName>
- <xref:System.Net.CookieContainer?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Net.Cookie`
- `T:System.Net.CookieContainer`

-->
