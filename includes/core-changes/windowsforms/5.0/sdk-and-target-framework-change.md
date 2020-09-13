---
ms.openlocfilehash: 975e331ad3e7bd7e0e8f49b62795c6acc7031ca9
ms.sourcegitcommit: 1e8382d0ce8b5515864f8fbb178b9fd692a7503f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89656322"
---
### <a name="winforms-and-wpf-apps-use-microsoftnetsdk"></a>Os aplicativos WinForms e WPF usam Microsoft. NET. Sdk

Os aplicativos Windows Forms e Windows Presentation Framework (WPF) agora usam o SDK do .NET ( `Microsoft.NET.Sdk` ) em vez do .NET Core WinForms e do SDK do WPF ( `Microsoft.NET.Sdk.WindowsDesktop` ).

#### <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET Core, os aplicativos WinForms e WPF usavam um [SDK de projeto](../../../../docs/core/project-sdk/overview.md) separado ( `Microsoft.NET.Sdk.WindowsDesktop` ). A partir do .NET 5,0, o SDK do WinForms e do WPF foi unificado com o SDK do .NET ( `Microsoft.NET.Sdk` ). Além disso, novos [monikers do Framework de destino (TFM)](../../../../docs/standard/frameworks.md) substituem `netcoreapp` e `netstandard` no .NET 5. O exemplo a seguir mostra as alterações que você precisaria fazer para um arquivo de projeto do WPF ao redirecionar para o .NET 5,0 ou posterior.

Nas versões anteriores do .NET Core:

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <UseWPF>true</UseWPF>
  </PropertyGroup>

</Project>
```

No .NET 5,0 e versões posteriores:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net5.0-windows</TargetFramework>
    <UseWPF>true</UseWPF>
  </PropertyGroup>

</Project>
```

#### <a name="version-introduced"></a>Versão introduzida

.NET 5,0 Preview 8

#### <a name="recommended-action"></a>Ação recomendada

No seu arquivo de projeto do WPF ou Windows Forms:

- Atualize o `Sdk` atributo para `Microsoft.NET.Sdk` .
- Atualize a `TargetFramework` propriedade para `net5.0-windows` .

#### <a name="category"></a>Categoria

- Windows Forms
- Windows Presentation Framework (WPF)

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!-- 

#### Affected APIs

Not detectable via API analysis.

-->
