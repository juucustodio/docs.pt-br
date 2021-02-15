---
title: Criar um pacote de modelos para dotnet new
description: Saiba como criar um arquivo csproj que criará um pacote de modelos para o comando dotnet new.
author: adegeo
ms.date: 12/11/2020
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 2aea143f1e41d580de41a9cc9e924d70b55695db
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633592"
---
# <a name="tutorial-create-a-template-pack"></a>Tutorial: criar um pacote de modelos

Com o .NET, você pode criar e implantar modelos que geram projetos, arquivos, até mesmo recursos. Este tutorial é a parte três de uma série que ensina a criar, instalar e desinstalar modelos para uso com o `dotnet new` comando.

Nesta parte da série, você aprenderá a:

> [!div class="checklist"]
>
> * Criar um \* projeto. csproj para criar um pacote de modelos
> * Configurar o arquivo de projeto para empacotamento
> * Instalar o modelo de um arquivo do pacote NuGet
> * Desinstalar um modelo pela ID do pacote

## <a name="prerequisites"></a>Pré-requisitos

* Conclua a [parte 1](cli-templates-create-item-template.md) e a [parte 2](cli-templates-create-project-template.md) desta série de tutoriais.

  Este tutorial usa os dois modelos criados nas duas primeiras partes deste tutorial. Você pode usar um modelo diferente, desde que copie o modelo, como uma pasta, na pasta _working\templates \\_ .

* Abra um terminal e navegue até a pasta de _trabalho \\_ .

## <a name="create-a-template-pack-project"></a>Criar um projeto de pacote de modelos

Um pacote de modelos é um ou mais modelos empacotados em um arquivo. Quando você instala ou desinstala um pacote, todos os modelos contidos no pacote são adicionados ou removidos, respectivamente. As partes anteriores desta série de tutoriais só funcionavam com modelos individuais. Para compartilhar um modelo não empacotado, você precisa copiar a pasta de modelos e instalá-la por meio dessa pasta. Como um pacote de modelos pode ter mais de um modelo e é um arquivo único, o compartilhamento é mais fácil.

Os pacotes de modelos são representados por um arquivo (_.nupkg_) do pacote NuGet. E, como qualquer pacote NuGet, você pode carregar o pacote de modelos em um feed do NuGet. O comando `dotnet new -i` dá suporte à instalação do pacote de modelos de um feed do pacote NuGet. Além disso, você pode instalar um pacote de modelos de um arquivo _.nupkg_ diretamente.

Normalmente você usa um arquivo de projeto C# para compilar o código e produzir um binário. No entanto, o projeto também pode ser usado para gerar um pacote de modelos. Com a alteração das configurações do _.csproj_, você pode evitar que ele compile códigos e, em vez disso, inclua todos os recursos dos modelos como recursos. Quando esse projeto é compilado, ele produz um pacote NuGet do pacote de modelos.

O pacote que você criará incluirá o [modelo de item](cli-templates-create-item-template.md) e o [modelo de pacote](cli-templates-create-project-template.md) criados anteriormente. Como agrupamos os dois modelos na pasta _working\templates\\_, podemos usar a pasta _working_ para o arquivo _.csproj_.

No terminal, navegue até a pasta _working_. Crie um novo projeto, defina o nome como `templatepack` e a pasta de saída para a pasta atual.

```dotnetcli
dotnet new console -n templatepack -o .
```

O `-n` parâmetro define o nome de arquivo _. csproj_ como _templatepack. csproj_. O `-o` parâmetro cria os arquivos no diretório atual. Você verá um resultado semelhante à seguinte saída.

```console
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on .\templatepack.csproj...
  Restore completed in 52.38 ms for C:\working\templatepack.csproj.

Restore succeeded.
```

Em seguida, abra o arquivo _templatepack.csproj_ em seu editor favorito e substitua o conteúdo pelo seguinte XML:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <PackageType>Template</PackageType>
    <PackageVersion>1.0</PackageVersion>
    <PackageId>AdatumCorporation.Utility.Templates</PackageId>
    <Title>AdatumCorporation Templates</Title>
    <Authors>Me</Authors>
    <Description>Templates to use when creating an application for Adatum Corporation.</Description>
    <PackageTags>dotnet-new;templates;contoso</PackageTags>

    <TargetFramework>netstandard2.0</TargetFramework>

    <IncludeContentInPack>true</IncludeContentInPack>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <ContentTargetFolders>content</ContentTargetFolders>
    <NoWarn>$(NoWarn);NU5128</NoWarn>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

As configurações `<PropertyGroup>` no XML acima estão divididas em três grupos. O primeiro grupo lida com as propriedades necessárias para um pacote NuGet. As três configurações `<Package*>` têm a ver com as propriedades do pacote NuGet para identificar seu pacote em um feed do NuGet. Especificamente, o valor `<PackageId>` é usado para desinstalar o pacote de modelos com um único nome em vez de um caminho de diretório. Ele também pode ser usado para instalar o pacote de modelos de um feed do NuGet. As configurações restantes, como `<Title>` e `<PackageTags>`, têm a ver com os metadados exibidos no feed do NuGet. Para saber mais sobre as configurações do NuGet, confira [Propriedades do NuGet e do MSBuild](/nuget/reference/msbuild-targets).

A configuração `<TargetFramework>` deve ser definida para que o MSBuild seja executado corretamente quando você executar o comando do pacote para compilar e empacotar o projeto.

As próximas três configurações devem ser feitas com a configuração correta do projeto para incluir os modelos na pasta apropriada no pacote NuGet quando ele é criado.

A última configuração suprime uma mensagem de aviso que não se aplica aos projetos do pacote de modelos.

O `<ItemGroup>` contém duas configurações. Primeiro, a configuração `<Content>` inclui tudo que se encontra na pasta _templates_ como conteúdo. Ele também é configurado para excluir a pasta _bin_ ou _obj_ para evitar que qualquer código compilado (se você testou e compilou seus modelos) seja incluído. Segundo, a configuração `<Compile>` exclui a compilação de todos os arquivos de código, independentemente de onde eles estejam localizados. Essa configuração impede que o projeto usado para criar um pacote de modelos tente compilar o código na hierarquia de pastas _templates_.

## <a name="build-and-install"></a>Compilar e instalar

Salve esse arquivo e execute o comando do pacote

```dotnetcli
dotnet pack
```

Esse comando criará seu projeto e criará um pacote NuGet. A pasta deve ser _working\bin\Debug_.

```dotnetcli
dotnet pack
```

```console
Microsoft (R) Build Engine version 16.8.0+126527ff1 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 123.86 ms for C:\working\templatepack.csproj.

  templatepack -> C:\working\bin\Debug\netstandard2.0\templatepack.dll
  Successfully created package 'C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg'.
```

Em seguida, instale o arquivo do pacote de modelos com o comando `dotnet new -i PATH_TO_NUPKG_FILE`.

```console
C:\working> dotnet new -i C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name               Language          Tags
--------------------------------------------      -------------------      ------------      ----------------------
Example templates: string extensions              stringext                [C#]              Common/Code
Console Application                               console                  [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync             [C#]              Common/Console/C#9
Class library                                     classlib                 [C#], F#, VB      Common/Library
```

Se você baixou o pacote NuGet para um feed do NuGet, é possível usar o comando `dotnet new -i PACKAGEID`, em que `PACKAGEID` é igual à configuração `<PackageId>` do arquivo _.csproj_. Essa ID do pacote é igual ao identificador do pacote NuGet.

## <a name="uninstall-the-template-pack"></a>Desinstalar o pacote de modelos

Não importa como você instalou o pacote de modelos, seja com o arquivo _.nupkg_ diretamente ou com o feed do NuGet, a remoção de um pacote de modelos é igual. Use o `<PackageId>` do modelo que você deseja desinstalar. Você pode obter uma lista de modelos instalados executando o comando `dotnet new -u`.

```dotnetcli
dotnet new -u
```

```console
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ProjectTemplates.2.2
    Details:
      NuGetPackageId: Microsoft.DotNet.Common.ProjectTemplates.2.2
      Version: 1.0.2-beta4
      Author: Microsoft
    Templates:
      Class library (classlib) C#
      Class library (classlib) F#
      Class library (classlib) VB
      Console Application (console) C#
      Console Application (console) F#
      Console Application (console) VB
    Uninstall Command:
      dotnet new -u Microsoft.DotNet.Common.ProjectTemplates.2.2

... cut to save space ...

  AdatumCorporation.Utility.Templates
    Details:
      NuGetPackageId: AdatumCorporation.Utility.Templates
      Version: 1.0.0
      Author: Me
    Templates:
      Example templates: async project (consoleasync) C#
      Example templates: string extensions (stringext) C#
    Uninstall Command:
      dotnet new -u AdatumCorporation.Utility.Templates
```

Execute `dotnet new -u AdatumCorporation.Utility.Templates` para desinstalar o modelo. O comando `dotnet new` gerará informações de ajuda que devem omitir os modelos que você instalou anteriormente.

Parabéns! você instalou e desinstalou um pacote de modelos.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre modelos, a maioria dos quais você já aprendeu, confira o artigo [Modelos personalizados para o dotnet new](../tools/custom-templates.md).

* [Wiki do repositório GitHub dotnet/modelagem](https://github.com/dotnet/templating/wiki)
* [Repositório do GitHub de dotnet/dotnet-template-samples](https://github.com/dotnet/dotnet-template-samples)
* [Esquema *template.json* no Repositório de Esquema JSON](http://json.schemastore.org/template)
