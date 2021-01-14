---
title: Processo de desenvolvimento para aplicativos baseados em Docker
description: Obtenha uma visão geral de alto nível das opções para o desenvolvimento de aplicativos baseados em Docker. Usando sua escolha do Visual Studio para Windows, Visual Studio para Mac ou Visual Studio Code para suporte multiplataforma (Windows, macOS e Linux).
ms.date: 01/13/2021
ms.openlocfilehash: 3a4f4078e745c52e8eca46473668e3319917bfd2
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188290"
---
# <a name="development-process-for-docker-based-applications"></a>Processo de desenvolvimento para aplicativos baseados em Docker

*Desenvolva aplicativos .NET em contêineres como você gosta, ou seja, o IDE (ambiente de desenvolvimento integrado) com foco no Visual Studio e nas ferramentas do Visual Studio para Docker ou CLI/editor voltado para a CLI do Docker e o Visual Studio Code.*

## <a name="development-environment-for-docker-apps"></a>Ambiente de desenvolvimento para aplicativos do Docker

### <a name="development-tool-choices-ide-or-editor"></a>Opções de ferramenta de desenvolvimento: IDE ou editor

Seja qual for a sua preferência, um IDE avançado e completo ou um editor leve e ágil, a Microsoft oferece as ferramentas que você pode usar para desenvolver aplicativos do Docker.

**Visual Studio (para Windows).** O desenvolvimento de aplicativos do .NET 5 baseado em Docker com o Visual Studio requer o Visual Studio 2019 versão 16,4 ou posterior. O Visual Studio 2019 vem com ferramentas para o Docker já incorporadas. As ferramentas para Docker permitem desenvolver, executar e validar seus aplicativos diretamente no ambiente do Docker de destino. Você pode pressionar F5 para executar e depurar seu aplicativo (contêiner único ou vários contêineres) diretamente em um host do Docker ou pressionar CTRL + F5 para editar e atualizar o aplicativo sem precisar recompilar o contêiner. Esse IDE é a opção de desenvolvimento mais potente para aplicativos baseados em Docker.

**Visual Studio para Mac.** É um IDE, evolução do Xamarin Studio, em execução no macOS. Para o desenvolvimento do .NET 5, é necessário ter a versão 8,4 ou posterior. Essa ferramenta deve ser a escolha preferida para os desenvolvedores que trabalham em máquinas macOS que também desejam usar um IDE potente.

**Visual Studio Code e a CLI do Docker**. Se preferir um editor leve e de plataforma cruzada que ofereça suporte a qualquer linguagem de desenvolvimento, você poderá usar Visual Studio Code e a CLI do Docker. Esse IDE é uma abordagem de desenvolvimento de plataforma cruzada para macOS, Linux e Windows. Além disso, o Visual Studio Code dá suporte às extensões do Docker, como IntelliSense para Dockerfiles e tarefas de atalho, para executar os comandos do Docker usando o editor.

Ao instalar a [Área de trabalho do Docker CE (Community Edition)](https://hub.docker.com/search/?type=edition&offering=community), você poderá usar uma única CLI do Docker para criar aplicativos para Windows e Linux.

### <a name="additional-resources"></a>Recursos adicionais

- **Do Visual Studio**. Site oficial. \
  [https://visualstudio.microsoft.com/vs/](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)

- **Visual Studio Code**. Site oficial. \
  <https://code.visualstudio.com/download>

- **Docker desktop para Windows Community Edition (CE)** \
  [https://hub.docker.com/editions/community/docker-ce-desktop-windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)

- **Docker desktop para Mac Community Edition (CE)** \
  [https://hub.docker.com/editions/community/docker-ce-desktop-mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)

## <a name="net-languages-and-frameworks-for-docker-containers"></a>Linguagens e estruturas do .NET para contêineres do Docker

Conforme mencionado nas seções anteriores deste guia, você pode usar .NET Framework, .NET 5 ou o projeto mono de código-fonte aberto ao desenvolver aplicativos .NET em contêineres do Docker. Você poderá desenvolver em C\#, em F\# ou em Visual Basic ao direcionar a contêineres do Linux ou do Windows, dependendo de qual .NET Framework estiver em uso. Para saber mais detalhes sobre as linguagens do .NET detalhes, consulte a postagem no blog [The .NET Language Strategy](https://devblogs.microsoft.com/dotnet/the-net-language-strategy/) (A estratégia de linguagem do .NET).

>[!div class="step-by-step"]
>[Anterior](../architect-microservice-container-applications/scalable-available-multi-container-microservice-applications.md) 
> [Avançar](docker-app-development-workflow.md)
