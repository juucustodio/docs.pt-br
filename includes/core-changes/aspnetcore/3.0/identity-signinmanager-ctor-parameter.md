---
ms.openlocfilehash: ed5a90063b8963d79f412ec1c5c0b9030f980f83
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032248"
---
### <a name="identity-signinmanager-constructor-accepts-new-parameter"></a>Identity: o Construtor SignInManager aceita o novo parâmetro

A partir do ASP.NET Core 3,0, um novo `IUserConfirmation<TUser>` parâmetro foi adicionado ao `SignInManager` Construtor. Para obter mais informações, consulte [dotnet/aspnetcore # 8356](https://github.com/dotnet/aspnetcore/issues/8356).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="reason-for-change"></a>Motivo da alteração

A motivação para a alteração foi adicionar suporte a novos fluxos de email/confirmação em identidade.

#### <a name="recommended-action"></a>Ação recomendada

Se você construir manualmente um `SignInManager` , forneça uma implementação de `IUserConfirmation` ou pegue uma de injeção de dependência a ser fornecida.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Identity.SignInManager%601.%23ctor%2A>

<!--

#### Affected APIs

`Overload:Microsoft.AspNetCore.Identity.SignInManager`1.#ctor`

-->
