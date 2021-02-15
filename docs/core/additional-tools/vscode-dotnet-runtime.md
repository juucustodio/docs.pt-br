---
title: Ferramenta de instalação do .NET para autores de extensão VS Code
description: Uma visão geral da ferramenta de instalação do .NET para autores de extensão, uma extensão Visual Studio Code para instalar o tempo de execução do .NET.
author: sfoslund
ms.date: 11/18/2020
ms.openlocfilehash: 37be1b9dcdb9fba99554800fea23f28443efb5fa
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599907"
---
# <a name="net-install-tool-for-extension-authors"></a>Ferramenta de instalação do .NET para autores de extensão

A [ferramenta de instalação do .net para autores de extensão](https://github.com/dotnet/vscode-dotnet-runtime) é uma extensão Visual Studio Code que permite a aquisição do tempo de execução do .net especificamente para autores de extensão vs Code. Essa ferramenta deve ser utilizada em extensões que são escritas em .NET e exigem que o .NET inicialize as partes da extensão (por exemplo, um servidor de idioma). A extensão não deve ser usada diretamente pelos usuários para instalar o .NET para desenvolvimento.

## <a name="getting-started-extension-authors"></a>Introdução: autores de extensão

Para garantir que a ferramenta de instalação do .NET para autores de extensão seja a melhor opção para seu cenário, comece revisando as [metas dessa extensão](https://github.com/dotnet/vscode-dotnet-runtime#goals-acquiring-net-core-for-extensions) em nossa página do github.

> [!NOTE]
> Essa ferramenta pode ser usada para instalar somente o tempo de execução do .NET, mas atualmente ele não tem a capacidade de instalar o SDK do .NET.

Depois de verificar se a ferramenta de instalação do .NET para autores de extensão atende às suas necessidades, você pode assumir uma dependência dele em seu [manifesto de extensão](https://code.visualstudio.com/api/references/extension-manifest) e começar a usar os comandos que expõemos com a [API vs Code](https://code.visualstudio.com/api/extension-guides/command#programmatically-executing-a-command). Você pode encontrar a lista de comandos que essa extensão expõe em nosso [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/blob/master/Documentation/commands.md).

Confira esta [extensão de exemplo](https://github.com/dotnet/vscode-dotnet-runtime/tree/master/sample) para ver essas etapas em ação.

Para obter mais exemplos, Confira essas extensões de software livre que atualmente aproveitam essa ferramenta:

- [Ferramentas do Azure Resource Manager (ARM) para Visual Studio Code](https://github.com/microsoft/vscode-azurearmtools)

- [Notebooks interativos do .NET](https://github.com/dotnet/interactive/tree/main/src/dotnet-interactive-vscode)

## <a name="getting-started-end-users"></a>Introdução: usuários finais

Em geral, o usuário final não deve precisar interagir com a ferramenta de instalação do .NET para autores de extensão. Se você estiver tendo problemas com a extensão, Confira nossa [página de solução de problemas](https://github.com/dotnet/vscode-dotnet-runtime/blob/master/Documentation/troubleshooting.md) ou arquivou um problema em nosso [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/issues).
