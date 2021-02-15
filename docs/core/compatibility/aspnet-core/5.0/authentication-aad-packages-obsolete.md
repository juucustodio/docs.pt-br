---
title: 'Alteração significativa: autenticação: AzureAD. UI e AzureADB2C. UI APIs e pacotes marcados como obsoletos'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 de autenticação: AzureAD. UI e AzureADB2C. UI APIs e pacotes marcados como obsoletos'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: c977ba4d6e34fc5f11133bdd1446a94d54efcb63
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760519"
---
# <a name="authentication-azureadui-and-azureadb2cui-apis-and-packages-marked-obsolete"></a>Autenticação: AzureAD. UI e AzureADB2C. UI APIs e pacotes marcados como obsoletos

No ASP.NET Core 2,1, a integração com o Azure Active Directory (Azure AD) e a autenticação Azure Active Directory B2C (Azure AD B2C) são fornecidas pelos pacotes [Microsoft. AspNetCore. Authentication. AzureAD. UI](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.AzureAD.UI) e [Microsoft. AspNetCore. Authentication. AzureADB2C. UI](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.AzureADB2C.UI) . A funcionalidade fornecida por esses pacotes é baseada no ponto de extremidade v 1.0 do Azure AD.

No ASP.NET Core 5,0 e posterior, a integração com o Azure AD e a autenticação Azure AD B2C é fornecida pelo pacote [Microsoft. Identity. Web](https://www.nuget.org/packages/Microsoft.Identity.Web) . Este pacote é baseado na plataforma de identidade da Microsoft, que é conhecida anteriormente como ponto de extremidade v 2.0 do Azure AD. Consequentemente, as APIs antigas nos `Microsoft.AspNetCore.Authentication.AzureAD.UI` `Microsoft.AspNetCore.Authentication.AzureADB2C.UI` pacotes e foram preteridas.

Para obter uma discussão, consulte o problema do GitHub [dotnet/aspnetcore # 25807](https://github.com/dotnet/aspnetcore/issues/25807).

## <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

## <a name="old-behavior"></a>Comportamento antigo

As APIs não estavam marcadas como obsoletas.

## <a name="new-behavior"></a>Novo comportamento

As APIs são marcadas como obsoletas.

## <a name="reason-for-change"></a>Motivo da alteração

A funcionalidade de autenticação do Azure AD e Azure AD B2C foi migrada para as APIs da MSAL (biblioteca de autenticação da Microsoft) fornecidas pelo `Microsoft.Identity.Web` .

## <a name="recommended-action"></a>Ação recomendada

Siga as `Microsoft.Identity.Web` diretrizes de API para [aplicativos Web](https://github.com/azuread/microsoft-identity-web/wiki/web-apps) e [APIs Web](https://github.com/azuread/microsoft-identity-web/wiki/web-apis).

## <a name="affected-apis"></a>APIs afetadas

* [Microsoft. AspNetCore. Authentication. AzureADAuthenticationBuilderExtensions](/dotnet/api/microsoft.aspnetcore.authentication.azureadauthenticationbuilderextensions?view=aspnetcore-3.0)
* [Microsoft. AspNetCore. Authentication. AzureAD. UI. AzureADDefaults](/dotnet/api/microsoft.aspnetcore.authentication.azuread.ui.azureaddefaults?view=aspnetcore-3.0)
* [Microsoft. AspNetCore. Authentication. AzureAD. UI. AzureADOptions](/dotnet/api/microsoft.aspnetcore.authentication.azuread.ui.azureadoptions?view=aspnetcore-3.0)
* [Microsoft. AspNetCore. Authentication. AzureADB2CAuthenticationBuilderExtensions](/dotnet/api/microsoft.aspnetcore.authentication.azureadb2cauthenticationbuilderextensions?view=aspnetcore-3.0)
* [Microsoft. AspNetCore. Authentication. AzureADB2C. UI. AzureADB2CDefaults](/dotnet/api/microsoft.aspnetcore.authentication.azureadb2c.ui.azureadb2cdefaults?view=aspnetcore-3.0)
* [Microsoft. AspNetCore. Authentication. AzureADB2C. UI. AzureADB2COptions](/dotnet/api/microsoft.aspnetcore.authentication.azureadb2c.ui.azureadb2coptions?view=aspnetcore-3.0)

<!--

### Category

ASP.NET Core

### Affected APIs

- `T:Microsoft.AspNetCore.Authentication.AzureADAuthenticationBuilderExtensions`
- `T:Microsoft.AspNetCore.Authentication.AzureAD.UI.AzureADDefaults`
- `T:Microsoft.AspNetCore.Authentication.AzureAD.UI.AzureADOptions`
- `T:Microsoft.AspNetCore.Authentication.AzureADB2CAuthenticationBuilderExtensions`
- `T:Microsoft.AspNetCore.Authentication.AzureADB2C.UI.AzureADB2CDefaults`
- `T:Microsoft.AspNetCore.Authentication.AzureADB2C.UI.AzureADB2COptions`

-->
