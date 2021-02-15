---
title: 'Alteração significativa: os aplicativos WinForms e WPF usam Microsoft. NET. Sdk'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que os aplicativos Windows Forms e Windows Presentation Framework agora usam o SDK do .NET em vez dos WinForms do .NET Core e do SDK do WPF.
ms.date: 09/18/2020
ms.openlocfilehash: 5eafed03fbf034f6a6457217a8527a877214e239
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633813"
---
# <a name="winforms-and-wpf-apps-use-microsoftnetsdk"></a>Os aplicativos WinForms e WPF usam Microsoft. NET. Sdk

Os aplicativos Windows Forms e Windows Presentation Framework (WPF) agora usam o SDK do .NET ( `Microsoft.NET.Sdk` ) em vez do .NET Core WinForms e do SDK do WPF ( `Microsoft.NET.Sdk.WindowsDesktop` ).

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET Core, os aplicativos WinForms e WPF usavam um [SDK de projeto](../../../project-sdk/overview.md) separado ( `Microsoft.NET.Sdk.WindowsDesktop` ). A partir do .NET 5,0, o SDK do WinForms e do WPF foi unificado com o SDK do .NET ( `Microsoft.NET.Sdk` ). Além disso, novos [monikers do Framework de destino (TFM)](../../../../standard/frameworks.md) substituem `netcoreapp` e `netstandard` no .NET 5. O exemplo a seguir mostra as alterações que você precisaria fazer para um arquivo de projeto do WPF ao redirecionar para o .NET 5,0 ou posterior.

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

## <a name="version-introduced"></a>Versão introduzida

SDK DO .NET 5.0.100

## <a name="recommended-action"></a>Ação recomendada

No seu arquivo de projeto do WPF ou Windows Forms:

- Atualize o `Sdk` atributo para `Microsoft.NET.Sdk` .
- Atualize a `TargetFramework` propriedade para `net5.0-windows` .

## <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

### Affected APIs

Not detectable via API analysis.

### Category

- Windows Forms
- Windows Presentation Framework (WPF)

-->
