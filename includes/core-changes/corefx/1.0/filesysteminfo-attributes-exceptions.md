---
ms.openlocfilehash: 2ea9abca7578c2ddf92712a1c597f8f1ff4a5c0c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031955"
---
### <a name="unauthorizedaccessexception-thrown-by-filesysteminfoattributes"></a>UnauthorizedAccessException gerado por FileSystemInfo. Attributes

No .NET Core, um <xref:System.UnauthorizedAccessException> é gerado quando o chamador tenta definir um valor de atributo de arquivo, mas não tem permissão de gravação.

#### <a name="change-description"></a>Descrição das alterações

No .NET Framework, um <xref:System.ArgumentException> é gerado quando o chamador tenta definir um valor de atributo de arquivo no <xref:System.IO.FileSystemInfo.Attributes?displayProperty=nameWithType> , mas não tem permissão de gravação. No .NET Core, um <xref:System.UnauthorizedAccessException> é lançado em vez disso. (No .NET Core, um <xref:System.ArgumentException> ainda será gerado se o chamador tentar definir um atributo de arquivo inválido.)

#### <a name="version-introduced"></a>Versão introduzida

1.0

#### <a name="recommended-action"></a>Ação recomendada

Modifique as `catch` instruções para capturar um <xref:System.UnauthorizedAccessException> em vez de, ou além de, um <xref:System.ArgumentException> , conforme necessário.

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.IO.FileSystemInfo.Attributes?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.IO.FileSystemInfo.Attributes`

-->
