---
ms.openlocfilehash: 6679e38aefa7d61ce430dc5375ff3b35c641ea27
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032246"
---
### <a name="identity-signinasync-throws-exception-for-unauthenticated-identity"></a>Identidade: o SignInAsync gera uma exceção para a identidade não autenticada

Por padrão, `SignInAsync` o gera uma exceção para entidades/identidades em que `IsAuthenticated` é `false` .

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

`SignInAsync` aceita quaisquer entidades/identidades, incluindo identidades em que `IsAuthenticated` é `false` .

#### <a name="new-behavior"></a>Novo comportamento

Por padrão, `SignInAsync` o gera uma exceção para entidades/identidades em que `IsAuthenticated` é `false` . Há um novo sinalizador para suprimir esse comportamento, mas o comportamento padrão foi alterado.

#### <a name="reason-for-change"></a>Motivo da alteração

O comportamento antigo era problemático porque, por padrão, essas entidades foram rejeitadas pelo `[Authorize]`  /  `RequireAuthenticatedUser()` .

#### <a name="recommended-action"></a>Ação recomendada

No ASP.NET Core 3,0 Preview 6, há um `RequireAuthenticatedSignIn` sinalizador `AuthenticationOptions` `true` por padrão. Defina esse sinalizador como `false` para restaurar o comportamento antigo.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
