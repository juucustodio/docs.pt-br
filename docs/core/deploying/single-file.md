---
title: Aplicativo de arquivo único
description: Saiba o que é um aplicativo de arquivo único e por que você deve considerar o uso desse modelo de implantação de aplicativo.
author: lakshanf
ms.author: lakshanf
ms.date: 08/28/2020
ms.openlocfilehash: 795ea98a9fd9d672b199eb2d9b24151340ef8246
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89495784"
---
# <a name="single-file-deployment-and-executable"></a>Implantação de arquivo único e executável

Agrupar todos os arquivos dependentes do aplicativo em um único binário fornece a um desenvolvedor de aplicativos a opção atrativa para implantar e distribuir o aplicativo como um único arquivo. Esse modelo de implantação está disponível desde o .NET Core 3,0 e foi aprimorado no .NET 5,0. Anteriormente no .NET Core 3,0, quando um usuário executa seu aplicativo de arquivo único, o host do .NET Core primeiro extrai todos os arquivos para um diretório temporário antes de executar o aplicativo. O .NET 5,0 melhora essa experiência executando diretamente o código sem a necessidade de extrair os arquivos do aplicativo.

A implantação de arquivo único está disponível tanto para o [modelo de implantação dependente de estrutura](index.md#publish-framework-dependent) quanto para [aplicativos independentes](index.md#publish-self-contained). O tamanho do único arquivo em um aplicativo independente será grande, já que incluirá o tempo de execução e as bibliotecas de estrutura. A opção de implantação de arquivo único pode ser combinada com as opções de publicação [ReadyToRun](../tools/dotnet-publish.md) e [Trim (um recurso experimental no .NET 5,0)](trim-self-contained.md) .

Há algumas advertências que você precisa estar ciente para o uso de arquivo único, primeiro do qual é o uso de informações de caminho para localizar um arquivo relativo ao local do seu aplicativo. A <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> API retornará uma cadeia de caracteres vazia, que é o comportamento padrão para assemblies carregados da memória. O compilador fornecerá um aviso para essa API durante o tempo de compilação para alertar o desenvolvedor sobre o comportamento específico. Se o caminho para o diretório do aplicativo for necessário, a <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType> API retornará o diretório onde o AppHost (o próprio pacote de arquivo único) reside. Os aplicativos C++ gerenciados não são adequados para implantação de arquivo único e recomendamos que você escreva aplicativos em C# para ser compatível com um único arquivo.

Por padrão, o arquivo único não agrupa bibliotecas nativas. No Linux, vinculamos o tempo de execução ao pacote e somente as bibliotecas nativas do aplicativo são implantadas no mesmo diretório que o aplicativo de arquivo único. No Windows, previnculo apenas o código de hospedagem e as bibliotecas nativas de tempo de execução e aplicativo são implantadas no mesmo diretório que o aplicativo de arquivo único. Isso é para garantir uma boa experiência de depuração, que exige que os arquivos nativos sejam excluídos do único arquivo. Há uma opção para definir um sinalizador, `IncludeNativeLibrariesForSelfExtract` , para incluir bibliotecas nativas no único pacote de arquivo, mas esses arquivos serão extraídos para um diretório temporário no computador cliente quando o aplicativo de arquivo único for executado.

## <a name="exclude-files-from-being-embedded"></a>Excluir arquivos de serem inseridos

Determinados arquivos podem ser explicitamente excluídos de serem inseridos no arquivo único definindo os seguintes metadados:

```xml
<ExcludeFromSingleFile>true</ExcludeFromSingleFile>
```

Por exemplo, para posicionar alguns arquivos no diretório de publicação, mas não agrupá-los no arquivo único:

```xml
<ItemGroup>
  <Content Update="Plugin.dll">
    <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
    <ExcludeFromSingleFile>true</ExcludeFromSingleFile>
  </Content>
</ItemGroup>
```

## <a name="publish-a-single-file-app---cli"></a>Publicar um aplicativo de arquivo único-CLI

Publicar um aplicativo de arquivo único usando o comando [dotnet Publish](../tools/dotnet-publish.md) . Ao publicar seu aplicativo, defina as seguintes propriedades:

- Publicar para um tempo de execução específico: `-r win-x64`
- Publicar como um arquivo único: `-p:PublishSingleFile=true`

O exemplo a seguir publica um aplicativo para o Windows como um aplicativo de arquivo único independente.

```dotnetcli
dotnet publish -r win-x64 -p:PublishSingleFile=true --self-contained true
```

O exemplo a seguir publica um aplicativo para Linux como um aplicativo de arquivo único dependente de estrutura.

```dotnetcli
dotnet publish -r linux-x64 -p:PublishSingleFile=true --self-contained false
```

Para obter mais informações, consulte [publicar aplicativos .NET Core com CLI do .NET Core](deploy-with-cli.md).

## <a name="publish-a-single-file-app---visual-studio"></a>Publicar um único aplicativo de arquivo-Visual Studio

O Visual Studio cria perfis de publicação reutilizáveis que controlam como seu aplicativo é publicado.

01. No painel **Gerenciador de soluções** , clique com o botão direito do mouse no projeto que você deseja publicar. Selecione **Publicar**.

    :::image type="content" source="media/single-file/visual-studio-solution-explorer.png" alt-text="Gerenciador de Soluções com um menu de clique com o botão direito do mouse, realçando a opção publicar.":::

    Se você ainda não tiver um perfil de publicação, siga as instruções para criar um e escolha o tipo de destino da **pasta** .

01. Escolha **Editar**.

    :::image type="content" source="media/single-file/visual-studio-publish-edit-settings.png" alt-text="Perfil de publicação do Visual Studio com o botão Editar.":::

01. Na caixa de diálogo **configurações de perfil** , defina as seguintes opções:

    - Defina o **modo de implantação** **como autônomo**.
    - Defina o **tempo de execução de destino** para a plataforma na qual você deseja publicar.
    - Selecione **produzir arquivo único**.

    Escolha **salvar** para salvar as configurações e retornar para a caixa de diálogo de **publicação** .

    :::image type="content" source="media/single-file/visual-studio-publish-single-file-properties.png" alt-text="Caixa de diálogo Configurações de perfil com modo de implantação, tempo de execução de destino e opções de arquivo único realçadas.":::

01. Escolha **publicar** para publicar seu aplicativo como um único arquivo.

Para obter mais informações, consulte [publicar aplicativos .NET Core com o Visual Studio](deploy-with-vs.md).

## <a name="publish-a-single-file-app---visual-studio-for-mac"></a>Publicar um único aplicativo de arquivo-Visual Studio para Mac

Visual Studio para Mac não fornece opções para publicar seu aplicativo como um único arquivo. Você precisará publicar manualmente seguindo as instruções da seção [publicar um único arquivo app-CLI](#publish-a-single-file-app---cli) . Para obter mais informações, consulte [publicar aplicativos .NET Core com CLI do .NET Core](deploy-with-cli.md).

## <a name="see-also"></a>Veja também

- [Implantação de aplicativo .NET Core](index.md).
- [Publicar aplicativos .NET Core com CLI do .NET Core](deploy-with-cli.md).
- [Publicar aplicativos .NET Core com o Visual Studio](deploy-with-vs.md).
- [ `dotnet publish` comando](../tools/dotnet-publish.md).
