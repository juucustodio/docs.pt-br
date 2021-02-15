---
ms.openlocfilehash: 60ebcd9fc9ca18c33d31b82ba5020426d22a7d5a
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032233"
---
### <a name="authentication-httpcontextauthentication-property-removed"></a>Autenticação: Propriedade HttpContext. Authentication removida

A propriedade preterida `Authentication` em `HttpContext` foi removida.

#### <a name="change-description"></a>Descrição das alterações

Como parte do [dotnet/aspnetcore # 6504](https://github.com/dotnet/aspnetcore/pull/6504), a propriedade preterida `Authentication` em `HttpContext` foi removida. A `Authentication` propriedade foi preterida desde 2,0. Um [Guia de migração](/aspnet/core/migration/1x-to-2x/identity-2x?view=aspnetcore-2.2#use-httpcontext-authentication-extensions) foi publicado para migrar o código usando essa propriedade preterida para as novas APIs de substituição. As classes/APIs não usadas restantes relacionadas à pilha de autenticação antiga ASP.NET Core 1. x foram removidas na confirmação [dotnet/aspnetcore@d7a7c65](https://github.com/dotnet/aspnetcore/commit/d7a7c65) .

Para obter uma discussão, consulte [dotnet/aspnetcore # 6533](https://github.com/dotnet/aspnetcore/issues/6533).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="reason-for-change"></a>Motivo da alteração

ASP.NET Core APIs 1,0 foram substituídas por métodos de extensão no <xref:Microsoft.AspNetCore.Authentication.AuthenticationHttpContextExtensions?displayProperty=fullName> .

#### <a name="recommended-action"></a>Ação recomendada

Consulte o [Guia de migração](/aspnet/core/migration/1x-to-2x/identity-2x?view=aspnetcore-2.2#use-httpcontext-authentication-extensions).

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.AspNetCore.Http.Authentication.AuthenticateInfo?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Authentication.AuthenticationManager?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Authentication.AuthenticationProperties?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Features.Authentication.AuthenticateContext?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Features.Authentication.ChallengeBehavior?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Features.Authentication.ChallengeContext?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Features.Authentication.DescribeSchemesContext?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Features.Authentication.IAuthenticationHandler?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Features.Authentication.IHttpAuthenticationFeature.Handler?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.Http.Features.Authentication.SignInContext?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Features.Authentication.SignOutContext?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.HttpContext.Authentication?displayProperty=fullName>

<!-- 

#### Affected APIs

- `T:Microsoft.AspNetCore.Http.Authentication.AuthenticateInfo`
- `T:Microsoft.AspNetCore.Http.Authentication.AuthenticationManager`
- `T:Microsoft.AspNetCore.Http.Authentication.AuthenticationProperties`
- `T:Microsoft.AspNetCore.Http.Features.Authentication.AuthenticateContext`
- `T:Microsoft.AspNetCore.Http.Features.Authentication.ChallengeBehavior`
- `T:Microsoft.AspNetCore.Http.Features.Authentication.ChallengeContext`
- `T:Microsoft.AspNetCore.Http.Features.Authentication.DescribeSchemesContext`
- `T:Microsoft.AspNetCore.Http.Features.Authentication.IAuthenticationHandler`
- `P:Microsoft.AspNetCore.Http.Features.Authentication.IHttpAuthenticationFeature.Handler`
- `T:Microsoft.AspNetCore.Http.Features.Authentication.SignInContext`
- `T:Microsoft.AspNetCore.Http.Features.Authentication.SignOutContext`
- `P:Microsoft.AspNetCore.Http.HttpContext.Authentication`

-->
