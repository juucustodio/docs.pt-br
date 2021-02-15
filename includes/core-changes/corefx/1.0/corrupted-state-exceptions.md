---
ms.openlocfilehash: 394f2daebad7b6af94bee4d7876796e87fe8ab19
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031953"
---
### <a name="handling-corrupted-state-exceptions-is-not-supported"></a>Não há suporte para a manipulação de exceções de estado corrompidas

Não há suporte para a manipulação de exceções de estado de processo corrompido no .NET Core.

#### <a name="change-description"></a>Descrição das alterações

Anteriormente, as exceções de estado de processo corrompido poderiam ser detectadas e manipuladas por manipuladores de exceção de código gerenciado, por exemplo, usando uma instrução [try-catch](../../../../docs/csharp/language-reference/keywords/try-catch.md) em C#.

A partir do .NET Core 1,0, as exceções de estado de processo corrompido não podem ser manipuladas pelo código gerenciado. O Common Language Runtime não entrega exceções de estado de processo corrompidas ao código gerenciado.

#### <a name="version-introduced"></a>Versão introduzida

1.0

#### <a name="recommended-action"></a>Ação recomendada

Evite a necessidade de lidar com exceções de estado de processo corrompido abordando as situações que levam a elas em vez disso. Se for absolutamente necessário manipular exceções de estado de processo corrompido, grave o manipulador de exceção em código C ou C++.

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute?displayProperty=fullName>
- [Elemento legacyCorruptedStateExceptionsPolicy](~/docs/framework/configure-apps/file-schema/runtime/legacycorruptedstateexceptionspolicy-element.md)

<!--

#### Affected APIs

- `T:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute`

-->
