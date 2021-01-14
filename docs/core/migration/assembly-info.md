---
title: Propriedades de AssemblyInfo
description: Saiba mais sobre atributos de assembly e como eles correspondem às propriedades do MSBuild no .NET Core 2,1 e versões posteriores.
ms.topic: reference
ms.date: 01/08/2021
ms.openlocfilehash: a2c431b3fe3da428f21582624ca5f357887e2815
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98192883"
---
# <a name="map-assemblyinfo-attributes-to-properties"></a>Mapear atributos AssemblyInfo para propriedades

Os [atributos de assembly](../../standard/assembly/set-attributes.md) que normalmente estavam presentes em um arquivo *AssemblyInfo* no .NET Core 2,0 e versões anteriores são gerados automaticamente a partir de propriedades do MSBuild, a partir do .NET Core 2,1.

## <a name="properties-per-attribute"></a>Propriedades por atributo

Conforme mostrado na tabela a seguir, cada atributo tem uma propriedade correspondente que controla seu conteúdo e outro que desabilita sua geração:

| Atributo                                                      | Propriedade               | Propriedade para desabilitar                             |
|----------------------------------------------------------------|------------------------|-------------------------------------------------|
| <xref:System.Reflection.AssemblyCompanyAttribute>              | `Company`              | `GenerateAssemblyCompanyAttribute`              |
| <xref:System.Reflection.AssemblyConfigurationAttribute>        | `Configuration`        | `GenerateAssemblyConfigurationAttribute`        |
| <xref:System.Reflection.AssemblyCopyrightAttribute>            | `Copyright`            | `GenerateAssemblyCopyrightAttribute`            |
| <xref:System.Reflection.AssemblyDescriptionAttribute>          | `Description`          | `GenerateAssemblyDescriptionAttribute`          |
| <xref:System.Reflection.AssemblyFileVersionAttribute>          | `FileVersion`          | `GenerateAssemblyFileVersionAttribute`          |
| <xref:System.Reflection.AssemblyInformationalVersionAttribute> | `InformationalVersion` | `GenerateAssemblyInformationalVersionAttribute` |
| <xref:System.Reflection.AssemblyProductAttribute>              | `Product`              | `GenerateAssemblyProductAttribute`              |
| <xref:System.Reflection.AssemblyTitleAttribute>                | `AssemblyTitle`        | `GenerateAssemblyTitleAttribute`                |
| <xref:System.Reflection.AssemblyVersionAttribute>              | `AssemblyVersion`      | `GenerateAssemblyVersionAttribute`              |
| <xref:System.Resources.NeutralResourcesLanguageAttribute>      | `NeutralLanguage`      | `GenerateNeutralResourcesLanguageAttribute`     |

Observações:

- `AssemblyVersion` e, `FileVersion` por padrão, o valor de `$(Version)` sem o sufixo. Por exemplo, se `$(Version)` fosse `1.2.3-beta.4`, então o valor seria `1.2.3`.
- `InformationalVersion` usa por padrão o valor de `$(Version)`.
- Se a `$(SourceRevisionId)` propriedade estiver presente, ela será anexada a `InformationalVersion` . Você pode desabilitar esse comportamento usando `IncludeSourceRevisionInInformationalVersion` .
- As propriedades `Copyright` e `Description` também são usadas para metadados do NuGet.
- `Configuration`, que usa como padrão o `Debug` é compartilhado com todos os destinos do MSBuild. Você pode defini-lo por meio da `--configuration` opção de `dotnet` comandos, por exemplo, [dotnet Pack](../tools/dotnet-pack.md).

## <a name="generateassemblyinfo"></a>GenerateAssemblyInfo

Um booliano que habilita ou desabilita a geração de AssemblyInfo. O valor padrão é `true`.

## <a name="generatedassemblyinfofile"></a>GeneratedAssemblyInfoFile

O caminho relativo ou absoluto do arquivo de informações do assembly gerado. O padrão é um arquivo chamado *[Project-Name]. AssemblyInfo. [cs | vb]* no `$(IntermediateOutputPath)` diretório (*obj*).
