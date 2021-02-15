---
title: Implantar aplicativos .NET no Raspberry Pi
description: Saiba como implantar aplicativos .NET no Raspberry Pi.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: how-to
ms.prod: dotnet
ms.openlocfilehash: 4da558e2cdfc283d21f2a5497cb71dc746109614
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96585639"
---
# <a name="deploy-net-apps-to-raspberry-pi"></a>Implantar aplicativos .NET no Raspberry Pi

A implantação de aplicativos .NET no Raspberry Pi é idêntica à de qualquer outra plataforma. Seu aplicativo pode ser executado como modo de implantação *independente* ou *dependente de estrutura* . Há vantagens para cada estratégia. Para obter mais informações, consulte [visão geral da publicação de aplicativos .net](../core/deploying/index.md).

## <a name="deploying-a-framework-dependent-app"></a>Implantando um aplicativo dependente de estrutura

Para implantar seu aplicativo como um aplicativo dependente de estrutura, conclua as seguintes etapas:

1. [!INCLUDE [ensure-ssh](includes/ensure-ssh.md)]

1. Instale o .NET no Raspberry Pi usando os [scripts dotnet-install](../core/tools/dotnet-install-script.md). Conclua as etapas a seguir em um prompt do bash no Raspberry Pi (local ou SSH):
    1. Execute o seguinte comando para instalar o .NET:

        ```bash
        curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin
        ```

        > [!NOTE]
        > Isso instala a versão mais recente. Se você precisar de uma versão específica, adicione `--version <VERSION>` ao final, em que `<VERSION>` é a versão de compilação específica.

    1. Para simplificar a resolução de caminho, adicione uma `DOTNET_ROOT` variável de ambiente e adicione o diretório *. dotnet* ao `$PATH` com os seguintes comandos:

        ```bash
        echo 'export DOTNET_ROOT=$HOME/.dotnet' >> ~/.bashrc
        echo 'export PATH=$PATH:$HOME/.dotnet' >> ~/.bashrc
        source ~/.bashrc
        ```

    1. Verifique a instalação do .NET com o seguinte comando:

        ```dotnetcli
        dotnet --version
        ```

        Verifique se a versão exibida corresponde à versão instalada.

1. Publique o aplicativo no computador de desenvolvimento da seguinte maneira, dependendo do ambiente de desenvolvimento.
    - Se estiver usando o **Visual Studio**, [implante o aplicativo em uma pasta local](/visualstudio/deployment/quickstart-deploy-to-local-folder?view=vs-2019). Antes de publicar, selecione **Editar** no resumo do perfil de publicação e selecione a guia **configurações** . Verifique se o **modo de implantação** está definido como dependente da *estrutura* e se o tempo de **execução de destino** está definido como *portátil*.
    - Se estiver usando a **CLI do .net**, use o comando [dotnet Publish](../core/tools/dotnet-publish.md) . Nenhum argumento adicional é necessário.

1. [!INCLUDE [sftp-client](includes/sftp-client.md)]

1. Em um prompt do bash no Raspberry Pi (local ou SSH), execute o aplicativo. Para fazer isso, defina a pasta de implantação como o diretório atual e execute o seguinte comando (em que *HelloWorld.dll* é o ponto de entrada do aplicativo):

    ```dotnetcli
    dotnet HelloWorld.dll
    ```

## <a name="deploying-a-self-contained-app"></a>Implantando um aplicativo independente

Para implantar seu aplicativo como um aplicativo independente, conclua as seguintes etapas:

1. [!INCLUDE [ensure-ssh](includes/ensure-ssh.md)]

1. Publique o aplicativo no computador de desenvolvimento da seguinte maneira, dependendo do ambiente de desenvolvimento.
    - Se estiver usando o **Visual Studio**, [implante o aplicativo em uma pasta local](/visualstudio/deployment/quickstart-deploy-to-local-folder?view=vs-2019). Antes de publicar, selecione **Editar** no resumo do perfil de publicação e selecione a guia **configurações** . Verifique se **o modo de implantação** está definido como independente e se o tempo *de* execução de **destino** está definido como *Linux-ARM*.
    - Se estiver usando a **CLI do .net**, use o comando [dotnet Publish](../core/tools/dotnet-publish.md) com o `-r linux-arm` argumento:

        ```dotnetcli
        dotnet publish -r linux-arm
        ```

1. [!INCLUDE [sftp-client](includes/sftp-client.md)]

1. Em um prompt do bash no Raspberry Pi (local ou SSH), execute o aplicativo. Para fazer isso, defina o diretório atual para o local de implantação e conclua as seguintes etapas:
    1. Forneça a permissão *executar* como executável (onde `HelloWorld` é o nome do arquivo executável).

        ```bash
        chmod +x HelloWorld
        ```

    1. Execute o executável.

        ```bash
        ./HelloWorld
        ```
