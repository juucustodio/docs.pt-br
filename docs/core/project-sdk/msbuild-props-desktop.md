---
title: Propriedades do MSBuild para Microsoft. NET. Sdk. desktop
description: Referência para as propriedades e os itens do MSBuild compreendidos pelo SDK de área de trabalho do .NET, que inclui WPF e WinForms.
ms.date: 02/04/2021
ms.topic: reference
author: adegeo
ms.author: adegeo
ms.custom: updateeachrelease
no-loc:
- App.xaml
- Application.xaml
- ApplicationDefinition
- Page
- EmbeddedResource
- Compile
- None
ms.openlocfilehash: 6d1903558dd03776a72eb6ee56ddae09fb66615b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488286"
---
# <a name="msbuild-reference-for-net-desktop-sdk-projects"></a>Referência do MSBuild para projetos do SDK de área de trabalho do .NET

Esta página é uma referência para as propriedades e os itens do MSBuild que você usa para configurar Windows Forms (WinForms) e Windows Presentation Foundation (WPF) projetos com o SDK de área de trabalho do .NET.

> [!NOTE]
> Este artigo documenta um subconjunto das propriedades do MSBuild para o SDK do .NET, pois ele se relaciona com os aplicativos da área de trabalho. Para obter uma lista de propriedades comuns do MSBuild do .NET SDK, consulte [referência do MSBuild para projetos do SDK do .net](msbuild-props.md). Para obter uma lista de propriedades comuns do MSBuild, consulte [Propriedades comuns do MSBuild](/visualstudio/msbuild/common-msbuild-project-properties).

## <a name="enable-net-desktop-sdk"></a>Habilitar o SDK de área de trabalho do .NET

Para usar WinForms ou WPF, configure o arquivo de projeto.

### <a name="net-50"></a>.NET 5.0

Especifique as seguintes configurações no arquivo de projeto do seu projeto do WinForms ou do WPF:

- Direcione o SDK do .NET `Microsoft.NET.Sdk` . Para obter mais informações, consulte [Project Files](overview.md#project-files).
- Defina [`TargetFramework`](msbuild-props.md#targetframework) como `net5.0-windows` .
- Adicione uma propriedade de estrutura de interface do usuário (ou ambas, se necessário):
  - Defina [`UseWPF`](#usewpf) como `true` para importar e usar o WPF.
  - Defina [`UseWindowsForms`](#usewindowsforms) como `true` para importar e usar WinForms.
- Adicional Defina `OutputType` como `WinExe` . Isso produz um aplicativo em oposição a uma biblioteca. Para produzir uma biblioteca, omita essa propriedade.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net5.0-windows</TargetFramework>

    <UseWPF>true</UseWPF>
    <!-- and/or -->
    <UseWindowsForms>true</UseWindowsForms>
  </PropertyGroup>

</Project>
```

### <a name="net-core-31"></a>.NET Core 3.1

Especifique as seguintes configurações no arquivo de projeto do seu projeto do WinForms ou do WPF:

- Direcione o SDK do .NET `Microsoft.NET.Sdk.WindowsDesktop` . Para obter mais informações, consulte [Project Files](overview.md#project-files).
- Defina [`TargetFramework`](msbuild-props.md#targetframework) como `netcoreapp3.1` .
- Adicione uma propriedade de estrutura de interface do usuário (ou ambas, se necessário):
  - Defina [`UseWPF`](#usewpf) como `true` para importar e usar o WPF.
  - Defina [`UseWindowsForms`](#usewindowsforms) como `true` para importar e usar WinForms.
- Adicional Defina `OutputType` como `WinExe` . Isso produz um aplicativo em oposição a uma biblioteca. Para produzir uma biblioteca, omita essa propriedade.

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>

    <UseWPF>true</UseWPF>
    <!-- and/or -->
    <UseWindowsForms>true</UseWindowsForms>
  </PropertyGroup>

</Project>
```

## <a name="wpf-default-includes-and-excludes"></a>Inclusões e exclusões padrão do WPF

Os projetos do SDK definem um conjunto de regras para incluir ou excluir arquivos implicitamente do projeto. Essas regras também definem automaticamente a ação de Build do arquivo. Isso é diferente dos projetos de .NET Framework não SDK mais antigos, que não têm regras de inclusão ou exclusão padrão. .NET Framework projetos exigem que você declare explicitamente quais arquivos incluir no projeto.

Os arquivos de projeto do .NET incluem um [conjunto padrão de regras](overview.md#default-includes-and-excludes) para processamento automático de arquivos. Os projetos do WPF adicionam mais regras.

A tabela a seguir mostra quais elementos e [globs](https://en.wikipedia.org/wiki/Glob_(programming)) são incluídos e excluídos no SDK da área de trabalho do .net quando a [`UseWPF`](#usewpf) Propriedade do projeto é definida como `true` :

| Elemento               | Incluir glob                 | Excluir glob                                                                                           | Remover glob  |
|-----------------------|------------------------------|--------------------------------------------------------------------|--------------|
| ApplicationDefinition | App.xaml ou Application.xaml | N/D                                                                | N/D          |
| Page                  | \*\*/\*. XAML                 | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc<br>Qualquer XAML definido por *ApplicationDefinition* | N/D          |
| None                  | N/D                          | N/D                                                                | \*\*/\*. XAML |

Aqui estão as configurações padrão include e Exclude para todos os tipos de projeto. Para obter mais informações, consulte [inclusões e exclusões padrão](overview.md#default-includes-and-excludes).

| Elemento           | Incluir glob                              | Excluir glob                                                  | Remover glob              |
|-------------------|-------------------------------------------|---------------------------------------------------------------|--------------------------|
| Compile           | \*\*/\*CS \*\*/\*. VB (ou outras extensões de linguagem) | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc  | N/D          |
| EmbeddedResource  | \*\*/\*.resx                              | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | N/D                      |
| None              | \*\*/\*                                   | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | \*\*/\*.cs; \*\*/\*.resx |

### <a name="errors-related-to-duplicate-items"></a>Erros relacionados a itens "duplicados"

Se você adicionou arquivos explicitamente ao seu projeto ou se tiver o XAML globs para incluir automaticamente arquivos em seu projeto, você poderá obter um dos seguintes erros:

* Itens ' ApplicationDefinition ' duplicados foram incluídos.
* Itens ' Page ' duplicados foram incluídos.

Esses erros são resultado da *inclusão* implícita de globs em conflito com suas configurações. Para contornar esse problema, defina [`EnableDefaultApplicationDefinition`](#enabledefaultapplicationdefinition) ou [`EnableDefaultPageItems`](#enabledefaultpageitems) como `false` . Definir esses valores como `false` reverter para o comportamento de SDKs anteriores em que você precisava definir explicitamente o globs padrão em seu projeto ou definir explicitamente os arquivos a serem incluídos no projeto.

Você pode desabilitar completamente todas as inclusões implícitas definindo a [ `EnableDefaultItems` Propriedade](msbuild-props.md#enabledefaultitems) como `false` .

## <a name="wpf-settings"></a>Configurações do WPF

- [UseWPF](#usewpf)
- [EnableDefaultApplicationDefinition](#enabledefaultapplicationdefinition)
- [EnableDefault Page itens](#enabledefaultpageitems)

Para obter informações sobre configurações de projeto não específicas do WPF, consulte [referência do MSBuild para projetos do SDK do .net](msbuild-props.md).

### <a name="usewpf"></a>UseWPF

A `UseWPF` propriedade controla se as referências às bibliotecas do WPF devem ser incluídas ou não. Isso também altera o pipeline do MSBuild para processar corretamente um projeto do WPF e arquivos relacionados. O valor padrão é `false`. Defina a `UseWPF` propriedade como `true` para habilitar o suporte do WPF. Você só pode direcionar a plataforma Windows quando essa propriedade estiver habilitada.

```xml
<PropertyGroup>
  <UseWPF>true</UseWPF>
</PropertyGroup>
```

Quando essa propriedade é definida como `true` , os projetos do .NET 5.0 + importarão automaticamente o [SDK da área de trabalho do .net](#enable-net-desktop-sdk).

Os projetos do .NET Core 3,1 precisam direcionar explicitamente o [SDK da área de trabalho do .net](#enable-net-desktop-sdk) para usar essa propriedade.

### <a name="enabledefaultapplicationdefinition"></a>EnableDefaultApplicationDefinition

A `EnableDefaultApplicationDefinition` propriedade controla se os `ApplicationDefinition` itens estão implicitamente incluídos no projeto. O valor padrão é `true`. Defina a `EnableDefaultApplicationDefinition` propriedade como `false` para desabilitar a inclusão de arquivo implícito.

```xml
<PropertyGroup>
  <EnableDefaultApplicationDefinition>false</EnableDefaultApplicationDefinition>
</PropertyGroup>
```

Essa propriedade requer que a propriedade [ `EnableDefaultItems` Property](msbuild-props.md#enabledefaultitems) seja definida como `true` , que é a configuração padrão.

### <a name="enabledefaultpageitems"></a>EnableDefault Page itens

A `EnableDefaultPageItems` propriedade controla se os `Page` itens, que são arquivos _. XAML_ , são incluídos implicitamente no projeto. O valor padrão é `true`. Defina a `EnableDefaultPageItems` propriedade como `false` para desabilitar a inclusão de arquivo implícito.

```xml
<PropertyGroup>
  <EnableDefaultPageItems>false</EnableDefaultPageItems>
</PropertyGroup>
```

Essa propriedade requer que a propriedade [ `EnableDefaultItems` Property](msbuild-props.md#enabledefaultitems) seja definida como `true` , que é a configuração padrão.

## <a name="windows-forms-settings"></a>Configurações de Windows Forms

- [UseWindowsForms](#usewindowsforms)

Para obter informações sobre propriedades de projeto específicas não WinForms, consulte [referência do MSBuild para projetos do SDK do .net](msbuild-props.md).

### <a name="usewindowsforms"></a>UseWindowsForms

A `UseWindowsForms` propriedade controla se seu aplicativo foi criado para o destino Windows Forms. Essa propriedade altera o pipeline do MSBuild para processar corretamente um projeto de Windows Forms e arquivos relacionados. O valor padrão é `false`. Defina a `UseWindowsForms` propriedade como `true` para habilitar Windows Forms suporte. Você só pode direcionar a plataforma Windows quando essa configuração estiver habilitada.

```xml
<PropertyGroup>
  <UseWindowsForms>true</UseWindowsForms>
</PropertyGroup>
```

Quando essa propriedade é definida como `true` , os projetos do .NET 5.0 + importarão automaticamente o [SDK da área de trabalho do .net](#enable-net-desktop-sdk).

Os projetos do .NET Core 3,1 precisam direcionar explicitamente o [SDK da área de trabalho do .net](#enable-net-desktop-sdk) para usar essa propriedade.

## <a name="shared-settings"></a>Configurações compartilhadas

- [DisableWinExeOutputInference](#disablewinexeoutputinference)

### <a name="disablewinexeoutputinference"></a>DisableWinExeOutputInference

Aplica-se ao SDK do .NET 5,0 e posterior.

Quando um aplicativo tiver o `Exe` valor definido para a `OutputType` propriedade, uma janela do console será criada se o aplicativo não estiver em execução em um console do. Esse geralmente não é o comportamento desejado de um aplicativo da área de trabalho do Windows. Com o `WinExe` valor, uma janela de console não é criada. A partir do SDK do .NET 5,0, o `Exe` valor é automaticamente transformado para `WinExe` .

A `DisableWinExeOutputInference` Propriedade reverte o comportamento de tratamento `Exe` como `WinExe` . Defina esse valor como `true` para restaurar o comportamento do `OutputType` valor da propriedade de `Exe` . O valor padrão é `false`.

```xml
<PropertyGroup>
  <DisableWinExeOutputInference>true</DisableWinExeOutputInference>
</PropertyGroup>
```

## <a name="see-also"></a>Consulte também

- [SDKs do projeto .NET](overview.md)
- [Referência do MSBuild para projetos do SDK do .NET](msbuild-props.md)
- [Referência de esquema do MSBuild](/visualstudio/msbuild/msbuild-project-file-schema-reference)
- [Propriedades comuns do MSBuild](/visualstudio/msbuild/common-msbuild-project-properties)
- [Personalizar uma compilação](/visualstudio/msbuild/customize-your-build)
