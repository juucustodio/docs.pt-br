---
ms.openlocfilehash: a4e20e0468d861138ad801c9dbfa15340b3f388c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032227"
---
### <a name="authentication-oauthhandler-exchangecodeasync-signature-changed"></a>Autenticação: assinatura OAuthHandler ExchangeCodeAsync alterada

No ASP.NET Core 3,0, a assinatura do `OAuthHandler.ExchangeCodeAsync` foi alterada de:

```csharp
protected virtual System.Threading.Tasks.Task<Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse> ExchangeCodeAsync(string code, string redirectUri) { throw null; }
```

Para:

```csharp
protected virtual System.Threading.Tasks.Task<Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse> ExchangeCodeAsync(Microsoft.AspNetCore.Authentication.OAuth.OAuthCodeExchangeContext context) { throw null; }
```

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

As `code` `redirectUri` cadeias de caracteres e foram passadas como argumentos separados.

#### <a name="new-behavior"></a>Novo comportamento

`Code` e `RedirectUri` são propriedades `OAuthCodeExchangeContext` que podem ser definidas por meio do `OAuthCodeExchangeContext` Construtor. O novo `OAuthCodeExchangeContext` tipo é o único argumento passado para `OAuthHandler.ExchangeCodeAsync` .

#### <a name="reason-for-change"></a>Motivo da alteração

Essa alteração permite que parâmetros adicionais sejam fornecidos de forma não-significativa. Não há necessidade de criar novas `ExchangeCodeAsync` sobrecargas.

#### <a name="recommended-action"></a>Ação recomendada

Construa um `OAuthCodeExchangeContext` com os `code` valores e apropriados `redirectUri` . Uma <xref:Microsoft.AspNetCore.Authentication.AuthenticationProperties> instância deve ser fornecida. Essa única `OAuthCodeExchangeContext` instância pode ser passada para `OAuthHandler.ExchangeCodeAsync` , em vez de vários argumentos.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Authentication.OAuth.OAuthHandler%601.ExchangeCodeAsync(System.String,System.String)?displayProperty=nameWithType>

<!--

#### Affected APIs

`M:Microsoft.AspNetCore.Authentication.OAuth.OAuthHandler`1.ExchangeCodeAsync(System.String,System.String)`

-->
