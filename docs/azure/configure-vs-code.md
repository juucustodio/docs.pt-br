---
title: Configurar Visual Studio Code para o desenvolvimento do Azure com o .NET
description: Este artigo ajuda você a configurar Visual Studio Code para o desenvolvimento do Azure, incluindo a obtenção dos plug-ins corretos instalados e configurados no VS Code
ms.date: 11/30/2020
ms.topic: conceptual
ms.custom: devx-track-dotnet
ms.author: daberry
author: daberry
ms.openlocfilehash: 65ced99befe12d137062b4ea6a59a1ccd3099e0b
ms.sourcegitcommit: 3d6d6595a03915f617349781f455f838a44b0f44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97701073"
---
# <a name="configure-visual-studio-code-for-azure-development"></a>Configurar Visual Studio Code para o desenvolvimento do Azure

Se você estiver usando Visual Studio Code, seja para o desenvolvimento do .NET, para criar aplicativos de página única usando estruturas como angular, reagir ou Vue ou para escrever aplicativos em outra linguagem, como o Python, você desejará configurar Visual Studio Code para o desenvolvimento do Azure.

### <a name="download-visual-studio-code"></a>Baixar o Visual Studio Code

Se você já tiver Visual Studio Code instalado, poderá ignorar esta etapa

> [!div class="nextstepaction"]
> [Baixar o Visual Studio Code](https://code.visualstudio.com/download)

### <a name="install-the-azure-tools-extension-pack"></a>Instalar o pacote de extensão das ferramentas do Azure

O [pacote de extensão das ferramentas do Azure](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) contém extensões para trabalhar com Azure app serviço, Azure functions, armazenamento do azure, Cosmos DB e máquinas virtuais do Azure, tudo em um pacote conveniente.

Para instalar a extensão de Visual Studio Code:

1. Pressione <kbd>Ctrl + Shift + X</kbd> para abrir a janela **extensões** .
1. Pesquise a extensão de *Ferramentas do Azure* .
1. Selecione o botão **Instalar**.

![Captura de tela da Visual Studio Code mostrando o painel de extensões pesquisando o pacote de extensão das ferramentas do Azure](./media/visual-studio-code-azure-tools.png)

Para saber mais sobre como instalar extensões no Visual Studio Code, consulte o documento de [extensão do Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery) no site do Visual Studio Code.

### <a name="sign-in-to-your-azure-account-with-azure-tools"></a>Entre em sua conta do Azure com as ferramentas do Azure

No painel esquerdo, você verá um ícone do Azure. Selecione esse ícone e um painel de controle para os serviços do Azure será exibido. Escolha **entrar no Azure...** em qualquer serviço para concluir o processo de autenticação das ferramentas do Azure no Visual Studio Code.

![Captura de tela do Visual Studio Code mostrando como fazer logon nas ferramentas do Azure para o Azure](./media/visual-studio-code-azure-login.png)

### <a name="next-steps"></a>Próximas etapas

Em seguida, você desejará instalar o CLI do Azure em sua estação de trabalho.

> [!div class="nextstepaction"]
> [Instalar a CLI do Azure](./install-azure-cli.md)
