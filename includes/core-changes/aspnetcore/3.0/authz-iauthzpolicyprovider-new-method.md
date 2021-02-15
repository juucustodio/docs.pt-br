---
ms.openlocfilehash: 58dbb73902c0226fa81acf1a70de2160f406f6c6
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032225"
---
### <a name="authorization-iauthorizationpolicyprovider-implementations-require-new-method"></a>Autorização: implementações de IAuthorizationPolicyProvider exigem novo método

No ASP.NET Core 3,0, um novo `GetFallbackPolicyAsync` método foi adicionado ao `IAuthorizationPolicyProvider` . Essa política de fallback é usada pelo middleware de autorização quando nenhuma política é especificada.

Para obter mais informações, consulte [dotnet/aspnetcore # 9759](https://github.com/dotnet/aspnetcore/pull/9759).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Implementações do `IAuthorizationPolicyProvider` não exigiam um `GetFallbackPolicyAsync` método.

#### <a name="new-behavior"></a>Novo comportamento

Implementações de `IAuthorizationPolicyProvider` exigem um `GetFallbackPolicyAsync` método.

#### <a name="reason-for-change"></a>Motivo da alteração

Um novo método era necessário para o novo `AuthorizationMiddleware` uso quando nenhuma política é especificada.

#### <a name="recommended-action"></a>Ação recomendada

Adicione o `GetFallbackPolicyAsync` método às suas implementações do `IAuthorizationPolicyProvider` .

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Authorization.IAuthorizationPolicyProvider?displayProperty=fullName>

<!-- 

#### Affected APIs

`T:Microsoft.AspNetCore.Authorization.IAuthorizationPolicyProvider`

-->
