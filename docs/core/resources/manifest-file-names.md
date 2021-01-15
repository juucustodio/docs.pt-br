---
title: Como o MSBuild gera nomes de arquivo de manifesto
description: Descreve os fatores que influenciam o nome de um nome de arquivo de manifesto de recurso gerado pelo MSBuild no momento da compilação.
ms.date: 05/08/2020
ms.topic: conceptual
ms.openlocfilehash: 2e0461e34bbd7f8da35bea1db1913a32915c7117
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970675"
---
# <a name="how-resource-manifest-files-are-named"></a>Como os arquivos de manifesto de recurso são nomeados

Quando o MSBuild compila um projeto do .NET Core, os arquivos de recursos XML, que têm a extensão de arquivo *. resx* , são convertidos em arquivos *. Resources* binários. Os arquivos binários são inseridos na saída do compilador e podem ser lidos pelo <xref:System.Resources.ResourceManager> . Este artigo descreve como o MSBuild escolhe um nome para cada arquivo *. Resources* .

> [!TIP]
> Se você adicionar explicitamente um item de recurso ao seu arquivo de projeto e ele também estiver [incluído com o padrão include globs for .NET Core](../project-sdk/overview.md#default-includes-and-excludes), você receberá um erro de compilação. Para incluir manualmente os arquivos de recurso como `EmbeddedResource` itens, defina a `EnableDefaultEmbeddedResourceItems` propriedade como false.

## <a name="default-name"></a>Nome padrão

No .NET Core 3,0 e posterior, o nome padrão de um manifesto de recurso é usado quando as duas condições a seguir são atendidas:

- O arquivo de recurso não é incluído explicitamente no arquivo de projeto como um `EmbeddedResource` item `LogicalName` com `ManifestResourceName` metadados, `DependentUpon` ou.
- A `EmbeddedResourceUseDependentUponConvention` propriedade não está definida como `false` no arquivo de projeto. Por padrão, essa propriedade é definida como `true`. Para obter mais informações, consulte [EmbeddedResourceUseDependentUponConvention](../project-sdk/msbuild-props.md#embeddedresourceusedependentuponconvention).

Se o arquivo de recurso for colocado com um arquivo de origem (*. cs* ou *. vb*) do mesmo nome de arquivo raiz, o nome completo do primeiro tipo definido no arquivo de origem será usado para o nome do arquivo de manifesto. Por exemplo, se `MyNamespace.Form1` for o primeiro tipo definido em *Form1.cs* e *Form1.cs* estiver colocalizado com *Form1. resx*, o nome de manifesto gerado para esse arquivo de recurso será *MyNamespace. Form1. Resources*.

## <a name="logicalname-metadata"></a>Metadados LogicalName

Se um arquivo de recurso estiver explicitamente incluído no arquivo de projeto como um `EmbeddedResource` item com `LogicalName` metadados, o `LogicalName` valor será usado como o nome do manifesto. `LogicalName` tem precedência sobre qualquer outro metadado ou configuração.

Por exemplo, o nome do manifesto para o arquivo de recurso que é definido no trecho de arquivo de projeto a seguir é *um somename. Resources*.

```xml
<EmbeddedResource Include="X.resx" LogicalName="SomeName.resources" />
```

- ou -

```xml
<EmbeddedResource Include="X.fr-FR.resx" LogicalName="SomeName.resources" />
```

## <a name="manifestresourcename-metadata"></a>Metadados do ManifestResourceName

Se um arquivo de recurso estiver explicitamente incluído no arquivo de projeto como um `EmbeddedResource` item com `ManifestResourceName` metadados (e `LogicalName` estiver ausente), o `ManifestResourceName` valor, combinado com a extensão de arquivo *. Resources*, será usado como o nome do arquivo de manifesto.

Por exemplo, o nome do manifesto para o arquivo de recurso que é definido no trecho de arquivo de projeto a seguir é *um somename. Resources*.

```xml
<EmbeddedResource Include="X.resx" ManifestResourceName="SomeName" />
```

O nome do manifesto para o arquivo de recurso que é definido no trecho de arquivo de projeto a seguir é *somename.fr-fr. Resources*.

```xml
<EmbeddedResource Include="X.fr-FR.resx" ManifestResourceName="SomeName.fr-FR" />
```

## <a name="dependentupon-metadata"></a>Metadados do DependentUpon

Se um arquivo de recurso estiver explicitamente incluído no arquivo de projeto como um `EmbeddedResource` item com `DependentUpon` metadados (e `LogicalName` e `ManifestResourceName` estiver ausente), as informações do arquivo de origem definido por `DependentUpon` são usadas para o nome do arquivo de manifesto de recurso. Especificamente, o nome do primeiro tipo que é definido no arquivo de origem é usado no nome do manifesto da seguinte maneira: *namespace. ClassName \[ . Culture]. Resources*.

Por exemplo, o nome do manifesto para o arquivo de recurso que é definido no trecho de arquivo de projeto a seguir é *namespace. ClassName. Resources* (em que `Namespace.Classname` é a primeira classe que é definida em *myTypes.cs*).

```xml
<EmbeddedResource Include="X.resx" DependentUpon="MyTypes.cs">
```

O nome do manifesto para o arquivo de recurso que é definido no trecho de arquivo de projeto a seguir é *namespace.ClassName.fr-fr. Resources* (em que `Namespace.Classname` é a primeira classe que é definida em *myTypes.cs*).

```xml
<EmbeddedResource Include="X.fr-FR.resx" DependentUpon="MyTypes.cs">
```

## <a name="embeddedresourceusedependentuponconvention-property"></a>Propriedade EmbeddedResourceUseDependentUponConvention

Se `EmbeddedResourceUseDependentUponConvention` é definido como `false` no arquivo de projeto, cada nome de arquivo de manifesto de recurso é baseado no namespace raiz do projeto e no caminho relativo da raiz do projeto para o arquivo *. resx* . Mais especificamente, o nome do arquivo de manifesto do recurso gerado é *RootNamespace. RelativePathWithDotsForSlashes. \[ Culture.] recursos* do. Essa também é a lógica usada para gerar nomes de manifesto em versões do .NET Core anteriores à 3,0.

> [!NOTE]
>
> - Se `RootNamespace` não estiver definido, o padrão será o nome do projeto.
> - Se `LogicalName` os `ManifestResourceName` metadados, ou `DependentUpon` forem especificados para um `EmbeddedResource` item no arquivo de projeto, essa regra de nomenclatura não se aplicará a esse arquivo de recurso.

## <a name="see-also"></a>Confira também

- [Como o nome do recurso de manifesto funciona](https://gist.github.com/BenVillalobos/041673b9a73bec60fdc3bf0f86fae62a)
- [Propriedades do MSBuild para projetos SDK do .NET Core](../project-sdk/msbuild-props.md)
- [Alterações interruptivas no MSBuild](../compatibility/msbuild.md)
