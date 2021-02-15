---
ms.openlocfilehash: e77312605ee367c159171e305d8f69429f9ac58b
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032247"
---
### <a name="identity-adddefaultui-method-overload-removed"></a>Identidade: sobrecarga do método AddDefaultUI removida

A partir do ASP.NET Core 3,0, a sobrecarga do método [IdentityBuilderUIExtensions. AddDefaultUI (IdentityBuilder, UIFramework)](/dotnet/api/microsoft.aspnetcore.identity.identitybuilderuiextensions.adddefaultui?view=aspnetcore-2.2#Microsoft_AspNetCore_Identity_IdentityBuilderUIExtensions_AddDefaultUI_Microsoft_AspNetCore_Identity_IdentityBuilder_Microsoft_AspNetCore_Identity_UI_UIFramework_) não existe mais.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi resultado da adoção do recurso de ativos da Web estáticos.

#### <a name="recommended-action"></a>Ação recomendada

Chame <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI(Microsoft.AspNetCore.Identity.IdentityBuilder)?displayProperty=nameWithType> em vez da sobrecarga que usa dois argumentos. Se você estiver usando a inicialização 3, adicione também a seguinte linha a um `<PropertyGroup>` elemento em seu arquivo de projeto:

```xml
<IdentityUIFrameworkVersion>Bootstrap3</IdentityUIFrameworkVersion>
```

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

[IdentityBuilderUIExtensions.AddDefaultUI(IdentityBuilder,UIFramework)](/dotnet/api/microsoft.aspnetcore.identity.identitybuilderuiextensions.adddefaultui?view=aspnetcore-2.2#Microsoft_AspNetCore_Identity_IdentityBuilderUIExtensions_AddDefaultUI_Microsoft_AspNetCore_Identity_IdentityBuilder_Microsoft_AspNetCore_Identity_UI_UIFramework_)

<!--

#### Affected APIs

`M:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI(Microsoft.AspNetCore.Identity.IdentityBuilder,Microsoft.AspNetCore.Identity.UI.UIFramework)`

-->
