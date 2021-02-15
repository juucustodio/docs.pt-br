---
title: Visão geral do SDK do .NET
description: Saiba mais sobre o SDK do .NET, que é um conjunto de bibliotecas e ferramentas usadas para criar projetos .NET.
ms.date: 07/31/2019
ms.technology: dotnet-cli
ms.openlocfilehash: 5236d4abec5dcbf950059dd906958158cfb592fe
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99216135"
---
# <a name="net-sdk-overview"></a>Visão geral do SDK do .NET

O SDK do .NET é um conjunto de bibliotecas e ferramentas que permitem aos desenvolvedores criar aplicativos e bibliotecas .NET. Ele contém os seguintes componentes que são usados para criar e executar aplicativos:

- A CLI do .NET.
- Bibliotecas e tempo de execução do .NET.
- O  [driver](tools/index.md#driver)`dotnet`.

## <a name="acquiring-the-net-sdk"></a>Adquirindo o SDK do .NET

Assim como acontece com qualquer ferramenta, o primeiro passo é obtê-la no seu computador. Dependendo do cenário, você pode instalar o SDK usando um dos seguintes métodos:

- Use os instaladores nativos.
- Use o script de shell de instalação.

Instaladores nativos destinam-se principalmente a computadores do desenvolvedor. O SDK é distribuído usando o mecanismo de instalação nativo de cada plataforma com suporte, como pacotes DEB no Ubuntu ou MSI no Windows. Esses instaladores instalam e configuram o ambiente conforme necessário para o usuário usar o SDK imediatamente após a instalação. No entanto, eles também exigem privilégios administrativos no computador. Você pode encontrar o SDK para instalar na página [Downloads do .NET](https://dotnet.microsoft.com/download).

Scripts de instalação, por outro lado, não exigem privilégios administrativos. No entanto, eles também não instalam nenhum pré-requisito no computador. Você precisa instalar todos os pré-requisitos manualmente. Os scripts destinam-se principalmente a configurar servidores de build ou para quando você deseja instalar as ferramentas sem privilégios de administrador (observe as limitações dos pré-requisitos acima). Veja mais informações no artigo de [referência do script de instalação](tools/dotnet-install-script.md). Se você estiver interessado em como configurar o SDK em seu servidor de Build de CI, consulte o artigo [usando o SDK do .net e as ferramentas no CI (integração contínua)](tools/using-ci-with-cli.md) .

Por padrão, o SDK é instalado de maneira "lado a lado" (SxS), o que significa que várias versões podem coexistir em um determinado momento em um único computador. A forma como a versão é escolhida quando você está executando comandos da CLI é explicada com mais detalhes no artigo [selecionar a versão do .net a ser usada](versions/selection.md) .

## <a name="see-also"></a>Confira também

- [Visão geral da CLI do .NET](tools/index.md)
- [Visão geral do controle de versão do .NET](versions/index.md)
- [Como remover o tempo de execução e o SDK do .NET](install/remove-runtime-sdk-versions.md)
- [Selecione a versão do .NET a ser usada](versions/selection.md)
