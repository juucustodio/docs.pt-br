---
title: 'Tutorial: instalar e usar uma ferramenta global do .NET'
description: Saiba como instalar e usar uma ferramenta .NET como uma ferramenta global.
ms.topic: tutorial
ms.date: 02/12/2020
ms.openlocfilehash: 01b773516da92fb16fb0f67fc6617e0c70d17c9d
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "94633888"
---
# <a name="tutorial-install-and-use-a-net-global-tool-using-the-net-cli"></a>Tutorial: instalar e usar uma ferramenta global do .NET usando a CLI do .NET

**Este artigo aplica-se a:** ✔️ SDK do .net Core 2,1 e versões posteriores

Este tutorial ensina como instalar e usar uma ferramenta global. Você usa uma ferramenta que você cria no [primeiro tutorial desta série](global-tools-how-to-create.md).

## <a name="prerequisites"></a>Pré-requisitos

* Conclua o [primeiro tutorial desta série](global-tools-how-to-create.md).

## <a name="use-the-tool-as-a-global-tool"></a>Usar a ferramenta como uma ferramenta global

1. Instale a ferramenta do pacote executando o comando [dotnet ferramenta de instalação](dotnet-tool-install.md) na pasta *Microsoft. botsay* Project:

   ```dotnetcli
   dotnet tool install --global --add-source ./nupkg microsoft.botsay
   ```

   O `--global` parâmetro informa à CLI do .net para instalar os binários da ferramenta em um local padrão que é adicionado automaticamente à variável de ambiente Path.

   O `--add-source` parâmetro informa à CLI do .net para usar temporariamente o diretório *./nupkg* como um feed de origem adicional para pacotes NuGet. Você deu ao seu pacote um nome exclusivo para certificar-se de que ele só será encontrado no diretório *./nupkg* , não no site do NuGet.org.

   A saída mostra o comando usado para chamar a ferramenta e a versão instalada:

   ```console
   You can invoke the tool using the following command: botsay
   Tool 'microsoft.botsay' (version '1.0.0') was successfully installed.
   ```

1. Invoque a ferramenta:

   ```console
   botsay hello from the bot
   ```

   > [!NOTE]
   > Se esse comando falhar, talvez seja necessário abrir um novo terminal para atualizar o caminho.

1. Remova a ferramenta executando o comando [dotnet ferramenta de desinstalação](dotnet-tool-uninstall.md) :

   ```dotnetcli
   dotnet tool uninstall -g microsoft.botsay
   ```

## <a name="use-the-tool-as-a-global-tool-installed-in-a-custom-location"></a>Usar a ferramenta como uma ferramenta global instalada em um local personalizado

1. Instale a ferramenta do pacote.

   No Windows:

   ```dotnetcli
   dotnet tool install --tool-path c:\dotnet-tools --add-source ./nupkg microsoft.botsay
   ```

   No Linux ou macOS:

   ```dotnetcli
   dotnet tool install --tool-path ~/bin --add-source ./nupkg microsoft.botsay
   ```

   O `--tool-path` parâmetro informa à CLI do .net para instalar os binários da ferramenta no local especificado. Se o diretório não existir, ele será criado. Esse diretório não é adicionado automaticamente à variável de ambiente PATH.

   A saída mostra o comando usado para chamar a ferramenta e a versão instalada:

   ```console
   You can invoke the tool using the following command: botsay
   Tool 'microsoft.botsay' (version '1.0.0') was successfully installed.
   ```

1. Invoque a ferramenta:

   No Windows:

   ```console
   c:\dotnet-tools\botsay hello from the bot
   ```

   No Linux ou macOS:

   ```console
   ~/bin/botsay hello from the bot
   ```

1. Remova a ferramenta executando o comando [dotnet ferramenta de desinstalação](dotnet-tool-uninstall.md) :

   No Windows:

   ```dotnetcli
   dotnet tool uninstall --tool-path c:\dotnet-tools microsoft.botsay
   ```

   No Linux ou macOS:

   ```dotnetcli
   dotnet tool uninstall --tool-path ~/bin microsoft.botsay
   ```

## <a name="troubleshoot"></a>Solução de problemas

Se você receber uma mensagem de erro ao seguir o tutorial, consulte [solucionar problemas de uso da ferramenta .net](troubleshoot-usage-issues.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você instalou e usou uma ferramenta como uma ferramenta global. Para instalar e usar a mesma ferramenta como uma ferramenta local, avance para o próximo tutorial.

> [!div class="nextstepaction"]
> [Instalar e usar ferramentas locais](local-tools-how-to-use.md)
