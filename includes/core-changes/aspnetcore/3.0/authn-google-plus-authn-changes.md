---
ms.openlocfilehash: 14d80f25c34465caa6dec10e5704fe0a3cbccc71
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96477956"
---
### <a name="authentication-google-deprecated-and-replaced"></a>Autenticação: Google + preterido e substituído

O Google está começando a [desligar](https://developers.google.com/+/api-shutdown) o Google + entrar para aplicativos como no início de 28 de janeiro de 2019.

#### <a name="change-description"></a>Descrição das alterações

ASP.NET 4. x e ASP.NET Core têm usado as APIs de entrada do Google + para autenticar usuários da conta do Google em aplicativos Web. Os pacotes NuGet afetados são [Microsoft. AspNetCore. Authentication. Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google/) para ASP.NET Core e [Microsoft. Owin. Security. Google](https://www.nuget.org/packages/Microsoft.Owin.Security.Google/) para `Microsoft.Owin` com ASP.NET Web Forms e MVC.

As APIs de substituição do Google usam uma fonte de dados e um formato diferentes. As atenuações e soluções fornecidas abaixo têm uma conta para as alterações estruturais. Os aplicativos devem verificar se os dados em si ainda atendem às suas necessidades. Por exemplo, nomes, endereços de email, links de perfil e fotos de perfil podem fornecer valores sutilmente diferentes de antes.

#### <a name="version-introduced"></a>Versão introduzida

Todas as versões. Essa alteração é externa a ASP.NET Core.

#### <a name="recommended-action"></a>Ação recomendada

##### <a name="owin-with-aspnet-web-forms-and-mvc"></a>Owin com ASP.NET Web Forms e MVC

Para `Microsoft.Owin` o 3.1.0 e posterior, uma mitigação temporária é descrita [aqui](https://github.com/aspnet/AspNetKatana/issues/251#issuecomment-449587635). Os aplicativos devem concluir o teste com a mitigação para verificar se há alterações no formato de dados. Há planos para lançar `Microsoft.Owin` o 4.0.1 com uma correção. Os aplicativos que usam qualquer versão anterior devem ser atualizados para a versão 4.0.1.

##### <a name="aspnet-core-1x"></a>ASP.NET Core 1.x

A mitigação no [Owin com ASP.NET Web Forms e MVC](#owin-with-aspnet-web-forms-and-mvc) pode ser adaptada para ASP.NET Core 1. x. Os patches do pacote NuGet não estão planejados porque 1. x atingiu o status [de término da vida útil](https://dotnet.microsoft.com/platform/support-policy) .

##### <a name="aspnet-core-2x"></a>ASP.NET Core 2.x

Para a `Microsoft.AspNetCore.Authentication.Google` versão 2. x, substitua sua chamada existente para `AddGoogle` in `Startup.ConfigureServices` pelo código a seguir:

```csharp
.AddGoogle(o =>
{
    o.ClientId = Configuration["Authentication:Google:ClientId"];
    o.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
    o.UserInformationEndpoint = "https://www.googleapis.com/oauth2/v2/userinfo";
    o.ClaimActions.Clear();
    o.ClaimActions.MapJsonKey(ClaimTypes.NameIdentifier, "id");
    o.ClaimActions.MapJsonKey(ClaimTypes.Name, "name");
    o.ClaimActions.MapJsonKey(ClaimTypes.GivenName, "given_name");
    o.ClaimActions.MapJsonKey(ClaimTypes.Surname, "family_name");
    o.ClaimActions.MapJsonKey("urn:google:profile", "link");
    o.ClaimActions.MapJsonKey(ClaimTypes.Email, "email");
});
```

Os patches de fevereiro de 2,1 e 2,2 incorporaram a reconfiguração anterior como o novo padrão. Nenhum patch está planejado para ASP.NET Core 2,0, pois ele atingiu o [fim da vida útil](https://dotnet.microsoft.com/platform/support-policy).

##### <a name="aspnet-core-30"></a>ASP.NET Core 3,0

A mitigação fornecida para o ASP.NET Core 2. x também pode ser usada para ASP.NET Core 3,0. Em futuras versões do 3,0, o `Microsoft.AspNetCore.Authentication.Google` pacote pode ser removido. Os usuários seriam direcionados para `Microsoft.AspNetCore.Authentication.OpenIdConnect` em vez disso. O código a seguir mostra como substituir `AddGoogle` por `AddOpenIdConnect` em `Startup.ConfigureServices` . Essa substituição pode ser usada com o ASP.NET Core 2,0 e posterior e pode ser adaptada para o ASP.NET Core 1. x, conforme necessário.

```csharp
.AddOpenIdConnect("Google", o =>
{
    o.ClientId = Configuration["Authentication:Google:ClientId"];
    o.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
    o.Authority = "https://accounts.google.com";
    o.ResponseType = OpenIdConnectResponseType.Code;
    o.CallbackPath = "/signin-google"; // Or register the default "/signin-oidc"
    o.Scope.Add("email");
});
JwtSecurityTokenHandler.DefaultInboundClaimTypeMap.Clear();
```

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Authentication.Google?displayProperty=fullName>

<!-- 

#### Affected APIs

`N:Microsoft.AspNetCore.Authentication.Google`

-->
