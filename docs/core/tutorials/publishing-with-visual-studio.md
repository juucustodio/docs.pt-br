---
title: Publicar um aplicativo de console .NET usando o Visual Studio
description: Saiba como usar o Visual Studio para criar o conjunto de arquivos necessários para executar um aplicativo .NET.
ms.date: 06/08/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet
ms.openlocfilehash: b0c6bd85ddf86f0eb11c56f01abb74a7e9786363
ms.sourcegitcommit: 5114e7847e0ff8ddb8c266802d47af78567949cf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94915987"
---
# <a name="tutorial-publish-a-net-console-application-using-visual-studio"></a>Tutorial: publicar um aplicativo de console .NET usando o Visual Studio

Este tutorial mostra como publicar um aplicativo de console para que outros usuários possam executá-lo. A publicação cria o conjunto de arquivos necessários para executar seu aplicativo. Para implantar os arquivos, copie-os para o computador de destino.

## <a name="prerequisites"></a>Pré-requisitos

- Este tutorial funciona com o aplicativo de console que você cria em [criar um aplicativo de console .NET usando o Visual Studio](with-visual-studio.md).

## <a name="publish-the-app"></a>Publicar o aplicativo

1. Inicie o Visual Studio.

1. Abra o projeto *HelloWorld* que você criou em [criar um aplicativo de console .NET usando o Visual Studio](with-visual-studio.md).

1. Verifique se o Visual Studio está usando a configuração de Build de versão. Se necessário, altere a configuração de build na barra de ferramentas de **Depuração** para **Lançamento**.

   :::image type="content" source="media/publishing-with-visual-studio/visual-studio-toolbar-release.png" alt-text="Barra de ferramentas do Visual Studio com build de versão selecionado":::

1. Clique com o botão direito do mouse no projeto **HelloWorld** (não na solução HelloWorld) e selecione **publicar** no menu.

   :::image type="content" source="media/publishing-with-visual-studio/publish-context-menu.png" alt-text="Menu de contexto Publicar do Visual Studio":::

1. Na guia **destino** da página **publicar** , selecione **pasta** e, em seguida, selecione **Avançar**.

   :::image type="content" source="media/publishing-with-visual-studio/pick-publish-target.png" alt-text="Escolher um destino de publicação no Visual Studio":::

1. Na guia **destino específico** da página **publicar** , selecione **pasta** e, em seguida, selecione **Avançar**.

   :::image type="content" source="media/publishing-with-visual-studio/pick-specific-publish-target.png" alt-text="Escolha o destino de publicação específico no Visual Studio":::

1. Na guia **local** da página **publicar** , selecione **concluir**.

   :::image type="content" source="media/publishing-with-visual-studio/publish-page-loc-tab.png" alt-text="Guia local da página de publicação do Visual Studio":::

1. Na guia **publicar** da janela **publicar** , selecione **publicar**.

   :::image type="content" source="media/publishing-with-visual-studio/publish-page.png" alt-text="Janela Publicar do Visual Studio":::

## <a name="inspect-the-files"></a>Inspecionar os arquivos

Por padrão, o processo de publicação cria uma implantação dependente de estrutura, que é um tipo de implantação em que o aplicativo publicado é executado no computador que tem o tempo de execução do .NET instalado. Os usuários podem executar o aplicativo publicado clicando duas vezes no executável ou emitindo o `dotnet HelloWorld.dll` comando de um prompt de comando.

Nas etapas a seguir, você examinará os arquivos criados pelo processo de publicação.

1. Em **Gerenciador de soluções**, selecione **Mostrar todos os arquivos**.

1. Na pasta do projeto, expanda *bin/Release/NET 5.0/publicar*.

   :::image type="content" source="media/publishing-with-visual-studio/published-files-output.png" alt-text="Gerenciador de Soluções mostrando os arquivos publicados":::

   Como mostra a imagem, a saída publicada inclui os seguintes arquivos:

   * *HelloWorld.deps.json*

      Este é o arquivo de dependências de tempo de execução do aplicativo. Ele define os componentes .NET e as bibliotecas (incluindo a biblioteca de vínculo dinâmico que contém seu aplicativo) necessárias para executar o aplicativo. Para obter mais informações, consulte [arquivos de configuração de tempo de execução](https://github.com/dotnet/cli/blob/85ca206d84633d658d7363894c4ea9d59e515c1a/Documentation/specs/runtime-configuration-file.md).

   * *HelloWorld.dll*

      Esta é a versão de [implantação dependente de estrutura](../deploying/deploy-with-cli.md#framework-dependent-deployment) do aplicativo. Para executar essa biblioteca de vínculo dinâmico, digite `dotnet HelloWorld.dll` em um prompt de comando. Esse método de execução do aplicativo funciona em qualquer plataforma que tenha o tempo de execução do .NET instalado.

   * *HelloWorld.exe*

      Esta é a versão [executável dependente de estrutura](../deploying/deploy-with-cli.md#framework-dependent-executable) do aplicativo. Para executá-lo, insira `HelloWorld.exe` em um prompt de comando. O arquivo é específico do sistema operacional.

   * *HelloWorld.pdb* (opcional para implantação)

      Este é o arquivo de símbolos de depuração. Não é necessário implantar esse arquivo juntamente com seu aplicativo, embora você deva salvá-lo caso precise depurar a versão publicada do seu aplicativo.

   * *HelloWorld.runtimeconfig.json*

      Este é o arquivo de configuração de tempo de execução do aplicativo. Ele identifica a versão do .NET na qual seu aplicativo foi criado para ser executado. Você também pode adicionar opções de configuração a ela. Para obter mais informações, consulte [definições de configuração de tempo de execução do .net](../run-time-config/index.md#runtimeconfigjson).

## <a name="run-the-published-app"></a>Executar o aplicativo publicado

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na pasta de *publicação* e selecione **Copiar caminho completo**.

1. Abra um prompt de comando e navegue até a pasta de *publicação* . Para fazer isso, insira `cd` e cole o caminho completo. Por exemplo:

   ```console
   cd C:\Projects\HelloWorld\bin\Release\netcoreapp3.1\publish\
   ```

1. Execute o aplicativo usando o executável:

   1. Insira `HelloWorld.exe` e pressione <kbd>Enter</kbd>.

   1. Insira um nome em resposta ao prompt e pressione qualquer tecla para sair.

1. Execute o aplicativo usando o `dotnet` comando:

   1. Insira `dotnet HelloWorld.dll` e pressione <kbd>Enter</kbd>.

   1. Insira um nome em resposta ao prompt e pressione qualquer tecla para sair.

## <a name="additional-resources"></a>Recursos adicionais

- [Implantação de aplicativos .NET](../deploying/index.md)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você publicou um aplicativo de console. No próximo tutorial, você criará uma biblioteca de classes.

> [!div class="nextstepaction"]
> [Criar uma biblioteca de classes .NET usando o Visual Studio](library-with-visual-studio.md)
