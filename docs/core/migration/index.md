---
title: Migração do .NET Core com project.json
description: Saiba como migrar um projeto .NET Core mais antigo usando project.json
ms.date: 07/19/2017
ms.openlocfilehash: 28da1723ed91d169305c2865c5346b8ce6e0b3d1
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189693"
---
# <a name="migrating-net-core-projects-from-projectjson"></a>Migração de projetos do .NET Core com project.json

Este documento aborda os três cenários de migração a seguir para projetos do .NET Core:

1. [Migração de um esquema válido mais recente do *project.json* para o *csproj*](#migration-from-projectjson-to-csproj)
2. [Migração do DNX para o csproj](#migration-from-dnx-to-csproj)
3. [Migração do RC3 e de projetos csproj anteriores do .NET Core para o formato final](#migration-from-earlier-net-core-csproj-formats-to-rtm-csproj)

Este documento só é aplicável a projetos do .NET Core mais antigos que usam project.jsno. Ele não se aplica à migração do .NET Framework para o .NET Core.

## <a name="migration-from-projectjson-to-csproj"></a>Migração do project.json para o csproj

A migração do *project.json* para o *.csproj* pode ser feita usando um dos seguintes métodos:

- [Visual Studio](#visual-studio)
- [ferramenta de linha de comando de migração do dotnet](#dotnet-migrate)

Ambos os métodos usam o mesmo mecanismo subjacente para migrar os projetos. Portanto, os resultados serão os mesmos. Na maioria dos casos, usar uma dessas duas maneiras de migrar o *project.js* de para *csproj* é a única coisa necessária e nenhuma outra edição manual do arquivo de projeto é necessária. O arquivo *.csproj* resultante terá o mesmo nome que o diretório contido.

### <a name="visual-studio"></a>Visual Studio

Quando você abre um arquivo *. xproj* ou um arquivo de solução que referencia arquivos *. Xproj* no Visual Studio 2017 ou no visual Studio 2019 versão 16,2 e anterior, a caixa de diálogo **atualização unidirecional** é exibida. A caixa de diálogo exibe os projetos a serem migrados. Se você abrir um arquivo de solução, todos os projetos especificados no arquivo de solução serão listados. Examine a lista de projetos a serem migrados e selecione **OK**.

![Caixa de diálogo Atualização unidirecional mostrando a lista de projetos que serão migrados](media/one-way-upgrade.jpg)

O Visual Studio migra os projetos selecionados automaticamente. Ao migrar uma solução, se você não escolher todos os projetos, a mesma caixa de diálogo será exibida solicitando que você atualize os projetos restantes dessa solução. Depois que o projeto for migrado, você poderá ver e modificar seu conteúdo clicando com o botão direito do mouse no projeto na janela **Gerenciador de soluções** e selecionando **Edit \<project name> . csproj**.

Os arquivos que foram migrados (*project.jsem*, *global.jsem*, *. xproj* e arquivo de solução) são movidos para uma pasta de *backup* . O arquivo de solução migrado é atualizado para o Visual Studio 2017 ou o Visual Studio 2019 e você não poderá abrir esse arquivo de solução no Visual Studio 2015 ou em versões anteriores. Um arquivo chamado *UpgradeLog.htm* que contém um relatório de migração também é salvo e aberto automaticamente.

> [!IMPORTANT]
> No Visual Studio 2019 versão 16,3 e posterior, você não pode carregar ou migrar um arquivo *. xproj* . Além disso, o Visual Studio 2015 não fornece a capacidade de migrar um arquivo *. xproj* . Se você estiver usando uma dessas versões do Visual Studio, instale uma versão adequada do Visual Studio ou use a ferramenta de migração de linha de comando descrita a seguir.

### <a name="dotnet-migrate"></a>dotnet migrate

No cenário de linha de comando, você pode usar o [`dotnet migrate`](../tools/dotnet-migrate.md) comando. Ele migra um projeto, uma solução ou um conjunto de pastas nessa ordem, dependendo de quais foram encontrados. Ao migrar um projeto, o projeto e todas as suas dependências são migrados.

Os arquivos que foram migrados (*project.json*, *global.json* e *. xproj*) são movidos para uma pasta de *backup* .

> [!NOTE]
> Se você estiver usando Visual Studio Code, o `dotnet migrate` comando não modificará arquivos específicos de Visual Studio Code, como *tasks.jsem*. Esses arquivos precisam ser alterados manualmente.
> Isso também será verdadeiro se você estiver usando um editor ou IDE (ambiente de desenvolvimento integrado) diferente do Visual Studio.

Consulte [um mapeamento entre project.jsPropriedades on e csproj](../tools/project-json-to-csproj.md) para uma comparação de *project.jsnos* formatos e *. csproj* .

Se houver um erro:

> Nenhum executável encontrado correspondendo ao comando dotnet-migrar

Execute `dotnet --version` para ver qual versão você está usando. [`dotnet migrate`](../tools/dotnet-migrate.md) foi introduzido no SDK do .NET Core 1.0.0 e removido na versão 3.0.100.
Você receberá esse erro se tiver um *global.jsno* arquivo no diretório atual ou pai, e a `sdk` versão que ele especifica estiver fora desse intervalo.

## <a name="migration-from-dnx-to-csproj"></a>Migração do DNX para o csproj

Se você ainda estiver usando o DNX para desenvolvimento no .NET Core, o processo de migração deverá ser feito em dois estágios:

1. Use as [diretrizes de migração existentes do DNX](from-dnx.md) para migrar do DNX para a CLI habilitada para project-json.
2. Siga as etapas da seção anterior para migrar do *project.json* para o *.csproj*.

> [!NOTE]
> O DNX foi preterido oficialmente durante a versão Visualização 1 da CLI do .NET Core.

## <a name="migration-from-earlier-net-core-csproj-formats-to-rtm-csproj"></a>Migração de formatos csproj anteriores do .NET Core para o csproj do RTM

O formato csproj do .NET Core foi mudando e evoluindo com cada nova versão de pré-lançamento da ferramenta. Não há nenhuma ferramenta que migrará seu arquivo de projeto de versões anteriores do csproj para a versão mais recente. Sendo assim, você precisa editar manualmente o arquivo de projeto. As etapas reais dependem da versão do arquivo de projeto que você está migrando. A seguir, há algumas diretrizes para serem consideradas com base nas alterações que ocorreram entre as versões:

- Remova a propriedade de versão das ferramentas do elemento `<Project>`, se ele existir.
- Remova o namespace de XML (`xmlns`) do elemento `<Project>`.
- Se ele não existir, adicione o atributo `Sdk` ao elemento `<Project>` e defina-o como `Microsoft.NET.Sdk` ou `Microsoft.NET.Sdk.Web`. Esse atributo especifica que o projeto usa o SDK que será utilizado. `Microsoft.NET.Sdk.Web` é usado em aplicativos Web.
- Remova as instruções `<Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />` e `<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />` da parte superior e inferior do projeto. Essas instruções estão implícitas no SDK. Portanto, não é necessário que elas estejam no projeto.
- Se você tiver `Microsoft.NETCore.App` ou `NETStandard.Library` `<PackageReference>` itens em seu projeto, deverá removê-los. Essas referências do pacote estão [implícitas no SDK](../project-sdk/overview.md).
- Remova o `Microsoft.NET.Sdk` `<PackageReference>` elemento, se ele existir. A referência do SDK é fornecida por meio do atributo `Sdk` no elemento `<Project>`.
- Remova os [globs](https://en.wikipedia.org/wiki/Glob_(programming)) que são [implícitos pelo SDK](../project-sdk/overview.md#default-includes-and-excludes). Deixar esses globs em seu projeto causará um erro no build, uma vez que os itens de compilação serão duplicados.

Após essas etapas, seu projeto deverá estar totalmente compatível com o formato csproj do RTM .NET Core.

Para obter exemplos de antes e depois da migração do formato csproj antigo para o novo, consulte o artigo [Updating Visual Studio 2017 RC – .NET Core Tooling improvements](https://devblogs.microsoft.com/dotnet/updating-visual-studio-2017-rc-net-core-tooling-improvements/) (Atualizando o Visual Studio 2017 RC – melhorias na ferramenta .NET Core) no blog do .NET.

## <a name="see-also"></a>Confira também

- [Portar, migrar e atualizar projetos do Visual Studio](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects)
