---
ms.openlocfilehash: 6af63c0a58a3273aa98fa70f22e3637b481806b4
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497187"
---
### <a name="path-colon-checks-are-stricter"></a>Verificações de dois-pontos em caminhos estão mais rigorosas

#### <a name="details"></a>Detalhes

No .NET Framework 4.6.2, uma série de alterações foram feitas para dar suporte aos caminhos incompatíveis anteriormente (em termos de comprimento e formato). Verifica se a sintaxe apropriada do separador de unidade (dois-pontos) foi feita mais corretamente, o que teve o efeito colateral de bloquear alguns caminhos de URI em algumas APIs de caminho SELECT em que foram toleradas anteriormente.

#### <a name="suggestion"></a>Sugestão

Ao passar um URI para as APIs afetadas, modifique a cadeia de caracteres para um caminho correto antes.

- Remova o esquema de URLs manualmente (por exemplo, remover `file://` das URLs).

- Passe o URI para a <xref:System.Uri> classe e use <xref:System.Uri.LocalPath> .

Como alternativa, você pode recusar a normalização de novo caminho definindo a `Switch.System.IO.UseLegacyPathHandling` opção AppContext como `true` .

| Nome    | Valor       |
|:--------|:------------|
| Escopo   | Microsoft Edge        |
| Versão | 4.6.2       |
| Tipo    | Redirecionando |

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.IO.Path.GetDirectoryName(System.String)?displayProperty=nameWithType>
- <xref:System.IO.Path.GetPathRoot(System.String)?displayProperty=nameWithType>
