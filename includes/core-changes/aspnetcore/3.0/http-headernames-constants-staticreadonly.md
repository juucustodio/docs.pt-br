---
ms.openlocfilehash: 31e7f84a787d255a474f4c2b1fa3068903dbed52
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032242"
---
### <a name="http-headernames-constants-changed-to-static-readonly"></a>Constantes HTTP: Headernames alteradas para static readonly

A partir do ASP.NET Core 3,0 Preview 5, os campos em <xref:Microsoft.Net.Http.Headers.HeaderNames?displayProperty=fullName> alterados de `const` para `static readonly` .

Para obter uma discussão, consulte [dotnet/aspnetcore # 9514](https://github.com/dotnet/aspnetcore/issues/9514).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Esses campos costumava ser `const` .

#### <a name="new-behavior"></a>Novo comportamento

Esses campos agora são `static readonly` .

#### <a name="reason-for-change"></a>Motivo da alteração

A alteração:

* Impede que os valores sejam inseridos entre limites de assembly, permitindo correções de valor conforme necessário.
* Permite verificações de igualdade de referência mais rápidas.

#### <a name="recommended-action"></a>Ação recomendada

Recompile em relação a 3,0. O código-fonte que usa esses campos das seguintes maneiras não pode mais fazer isso:

* Como um argumento de atributo
* Como um `case` em uma `switch` instrução
* Ao definir outro `const`

Para contornar a alteração significativa, alterne para usando constantes de nome de cabeçalho autodefinido ou literais de cadeia de caracteres.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.Net.Http.Headers.HeaderNames?displayProperty=fullName>

<!-- 

#### Affected APIs

`T:Microsoft.Net.Http.Headers.HeaderNames`

-->
