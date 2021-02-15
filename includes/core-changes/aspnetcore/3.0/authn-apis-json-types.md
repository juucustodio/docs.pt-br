---
ms.openlocfilehash: 9bdfcca2fd03e24a636be3340f5057dc3f39358e
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032234"
---
### <a name="authentication-newtonsoftjson-types-replaced"></a>Autenticação: Newtonsoft.Jsem tipos substituídos

No ASP.NET Core 3,0, os `Newtonsoft.Json` tipos usados em APIs de autenticação foram substituídos por `System.Text.Json` tipos. Exceto pelos seguintes casos, o uso básico dos pacotes de autenticação permanece inalterado:

* Classes derivadas de provedores OAuth, como as de [ASPNET-contrib](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers).
* Implementações avançadas de manipulação de declaração.

Para obter mais informações, consulte [dotnet/aspnetcore # 7105](https://github.com/dotnet/aspnetcore/pull/7105). Para obter uma discussão, consulte [dotnet/aspnetcore # 7289](https://github.com/dotnet/aspnetcore/issues/7289).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="recommended-action"></a>Ação recomendada

Para implementações de OAuth derivadas, a alteração mais comum é substituir `JObject.Parse` por `JsonDocument.Parse` na `CreateTicketAsync` substituição, conforme mostrado [aqui](https://github.com/dotnet/aspnetcore/pull/7105/files?utf8=%E2%9C%93&diff=unified&w=1#diff-e1c9f9740a6fe8021020a6f249c589b0L40). `JsonDocument` implementa `IDisposable`.

A lista a seguir descreve as alterações conhecidas:

- <xref:Microsoft.AspNetCore.Authentication.OAuth.Claims.ClaimAction.Run(Newtonsoft.Json.Linq.JObject,System.Security.Claims.ClaimsIdentity,System.String)?displayProperty=nameWithType> se torna `ClaimAction.Run(JsonElement userData, ClaimsIdentity identity, string issuer)` . Todas as implementações derivadas do `ClaimAction` são afetadas de forma semelhante.
- <xref:Microsoft.AspNetCore.Authentication.ClaimActionCollectionMapExtensions.MapCustomJson(Microsoft.AspNetCore.Authentication.OAuth.Claims.ClaimActionCollection,System.String,System.Func{Newtonsoft.Json.Linq.JObject,System.String})?displayProperty=nameWithType> torna-se `MapCustomJson(this ClaimActionCollection collection, string claimType, Func<JsonElement, string> resolver)`
- <xref:Microsoft.AspNetCore.Authentication.ClaimActionCollectionMapExtensions.MapCustomJson(Microsoft.AspNetCore.Authentication.OAuth.Claims.ClaimActionCollection,System.String,System.String,System.Func{Newtonsoft.Json.Linq.JObject,System.String})?displayProperty=nameWithType> torna-se `MapCustomJson(this ClaimActionCollection collection, string claimType, string valueType, Func<JsonElement, string> resolver)`
- <xref:Microsoft.AspNetCore.Authentication.OAuth.OAuthCreatingTicketContext> teve um Construtor antigo removido e o outro foi substituído `JObject` por `JsonElement` . A `User` propriedade e o `RunClaimActions` método foram atualizados para corresponder.
- <xref:Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse.Success(Newtonsoft.Json.Linq.JObject)> Agora aceita um parâmetro do tipo `JsonDocument` em vez de `JObject` . A `Response` propriedade foi atualizada para corresponder. `OAuthTokenResponse` Agora é descartável e será Descartado pelo `OAuthHandler` . A substituição de implementações OAuth derivadas `ExchangeCodeAsync` não precisa descartar o `JsonDocument` ou o `OAuthTokenResponse` .
- <xref:Microsoft.AspNetCore.Authentication.OpenIdConnect.UserInformationReceivedContext.User?displayProperty=nameWithType> alterado de `JObject` para `JsonDocument` .
- <xref:Microsoft.AspNetCore.Authentication.Twitter.TwitterCreatingTicketContext.User?displayProperty=nameWithType> alterado de `JObject` para `JsonElement` .
- O último parâmetro de [TwitterHandler. CreateTicketAsync (ClaimsIdentity, authenticationproperties, AccessToken, JObject)](/dotnet/api/microsoft.aspnetcore.authentication.twitter.twitterhandler.createticketasync?view=aspnetcore-2.2#Microsoft_AspNetCore_Authentication_Twitter_TwitterHandler_CreateTicketAsync_System_Security_Claims_ClaimsIdentity_Microsoft_AspNetCore_Authentication_AuthenticationProperties_Microsoft_AspNetCore_Authentication_Twitter_AccessToken_Newtonsoft_Json_Linq_JObject_) foi alterado de `JObject` para `JsonElement` . O método de substituição é <xref:Microsoft.AspNetCore.Authentication.Twitter.TwitterHandler.CreateTicketAsync(System.Security.Claims.ClaimsIdentity,Microsoft.AspNetCore.Authentication.AuthenticationProperties,Microsoft.AspNetCore.Authentication.Twitter.AccessToken,System.Text.Json.JsonElement)?displayProperty=nameWithType> .

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.AspNetCore.Authentication.Facebook?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Authentication.Google?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Authentication.MicrosoftAccount?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Authentication.OAuth?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Authentication.OpenIdConnect?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Authentication.Twitter?displayProperty=nameWithType>

<!--

#### Affected APIs

- `N:Microsoft.AspNetCore.Authentication.Facebook`
- `N:Microsoft.AspNetCore.Authentication.Google`
- `N:Microsoft.AspNetCore.Authentication.MicrosoftAccount`
- `N:Microsoft.AspNetCore.Authentication.OAuth`
- `N:Microsoft.AspNetCore.Authentication.OpenIdConnect`
- `N:Microsoft.AspNetCore.Authentication.Twitter`

-->
