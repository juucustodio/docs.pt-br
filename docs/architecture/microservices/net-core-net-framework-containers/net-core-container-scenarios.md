---
title: Quando escolher o .NET 5 para contêineres do Docker
description: Arquitetura de microserviços .NET para aplicativos .NET em contêineres | Quando escolher o .NET para contêineres do Docker
ms.date: 02/02/2021
ms.openlocfilehash: d0480ac43c0090b72185bd23bbd11ac7e26001e6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99653414"
---
# <a name="when-to-choose-net-for-docker-containers"></a>Quando escolher o .NET para os contêineres do Docker

A modularidade e a natureza leve do .NET 5 tornam-as perfeitos para contêineres. Quando você implanta e inicia um contêiner, sua imagem é muito menor com o .NET 5 do que com .NET Framework. Por outro lado, para usar .NET Framework para um contêiner, você deve basear sua imagem na imagem do Windows Server Core, que é muito mais pesada do que as imagens do Windows nano Server ou do Linux que você usa para o .NET 5.

Além disso, o .NET 5 é de plataforma cruzada, para que você possa implantar aplicativos de servidor com imagens de contêiner do Linux ou do Windows. No entanto, se você estiver usando o .NET Framework tradicional, só poderá implantar imagens baseadas no Windows Server Core.

Veja a seguir uma explicação mais detalhada de por que escolher o .NET 5.

## <a name="developing-and-deploying-cross-platform"></a>Desenvolvendo e implantando uma multiplataforma

Claramente, se seu objetivo for ter um aplicativo (aplicativo Web ou serviço) que possa ser executado em várias plataformas compatíveis com o Docker (Linux e Windows), a escolha certa é o .NET 5, porque .NET Framework só oferece suporte ao Windows.

O .NET 5 também oferece suporte a macOS como uma plataforma de desenvolvimento. No entanto, quando você implanta contêineres em um host do Docker, esse host deve (atualmente) ser baseado em Linux ou Windows. Por exemplo, em um ambiente de desenvolvimento, você pode usar uma VM Linux em execução em um Mac.

O [Visual Studio](https://www.visualstudio.com/vs/) fornece um IDE (ambiente de desenvolvimento integrado) para Windows e é compatível com o desenvolvimento do Docker.

O [Visual Studio para Mac](https://www.visualstudio.com/vs/visual-studio-mac/) é um IDE, a evolução do Xamarin Studio, que é executada em macOS e dá suporte ao desenvolvimento de aplicativos baseados em Docker. Essa ferramenta deve ser a escolha preferida para os desenvolvedores que trabalham em máquinas Mac que também desejam usar um IDE potente.

Você também pode usar [Visual Studio Code](https://code.visualstudio.com/) no MacOS, Linux e Windows. Visual Studio Code oferece suporte total ao .NET 5, incluindo IntelliSense e depuração. Como VS Code é um editor leve, você pode usá-lo para desenvolver aplicativos em contêineres no computador em conjunto com a CLI do Docker e a [CLI do .net](../../../core/tools/index.md). Você também pode direcionar o .NET 5 com a maioria dos editores de terceiros, como sublime, Emacs, vi e o projeto OmniSharp de código-fonte aberto, que também fornece suporte ao IntelliSense.

Além dos IDEs e editores, você pode usar a CLI do [.net](../../../core/tools/index.md) para todas as plataformas com suporte.

## <a name="using-containers-for-new-green-field-projects"></a>Usando contêineres para novos projetos ("campo verde")

Contêineres são comumente usados em conjunto com uma arquitetura de microsserviços, embora também possam ser usados para colocar em contêineres aplicativos Web ou serviços que sigam qualquer padrão de arquitetura. Você pode usar .NET Framework em contêineres do Windows, mas a modularidade e a natureza leve do .NET 5 tornam-o perfeita para as arquiteturas de contêineres e de microserviços. Quando você cria e implanta um contêiner, sua imagem é muito menor com o .NET 5 do que com .NET Framework.

## <a name="create-and-deploy-microservices-on-containers"></a>Criar e implantar microserviços em contêineres

É possível usar o .NET Framework tradicional para criar aplicativos baseados em microsserviços (sem contêineres) usando processos simples. Dessa forma, como o .NET Framework já está instalado e já é compartilhado entre processos, os processos são leves inicializam rapidamente. No entanto, se você estiver usando contêineres, a imagem do .NET Framework tradicional também será baseada no Windows Server Core e isso a tornará muito pesada para uma abordagem de microsserviços em contêineres. No entanto, as equipes têm busca de oportunidades para melhorar a experiência de .NET Framework usuários também. Recentemente, o tamanho das [imagens de contêiner do Windows Server Core foi reduzido para >40% menor](https://devblogs.microsoft.com/dotnet/we-made-windows-server-core-container-images-40-smaller).

Por outro lado, o .NET 5 é o melhor candidato se você estiver adotando um sistema orientado a microserviços baseado em contêineres, pois o .NET 5 é leve. Além disso, suas imagens de contêiner relacionadas, para Linux ou Windows nano Server, são de baixo e pequeno, tornando os contêineres claros e rápidos para começar.

Um microsserviço deve ser o menor possível: ser leve ao iniciar, ocupar um pequeno espaço, ter um Contexto limitado pequeno (confira DDD, [Design Voltado a Domínio](https://en.wikipedia.org/wiki/Domain-driven_design)), para representar uma pequena área de preocupações e ser capaz de ser iniciado e interrompido rapidamente. Para esses requisitos, você desejará usar imagens de contêiner pequenas e rápidas para instanciar, como a imagem de contêiner do .NET 5.

Uma arquitetura de microsserviços também permite uma combinação de tecnologias em um limite de serviço. Essa abordagem permite uma migração gradual para o .NET 5 para novos microserviços que funcionam em conjunto com outros microserviços ou com serviços desenvolvidos com Node.js, Python, Java, GoLang ou outras tecnologias.

## <a name="deploying-high-density-in-scalable-systems"></a>Implantando alta densidade em sistemas escalonáveis

Quando o sistema baseado em contêiner precisa da melhor densidade possível, granularidade e desempenho, o .NET e o ASP.NET Core são as melhores opções. O ASP.NET Core é até 10 vezes mais rápido do que o ASP.NET na .NET Framework tradicional, e ele lidera outras tecnologias populares do setor para os microserviços, como Servlets Java, Go e Node.js.

Essa abordagem é especialmente relevante para arquiteturas de microserviço, em que você pode ter centenas de microserviços (contêineres) em execução. Com as imagens de ASP.NET Core (com base no tempo de execução do .NET) no Linux ou no Windows nano, você pode executar o sistema com um número muito menor de servidores ou VMs, poupando, em última análise, os custos em infraestrutura e hospedagem.

>[!div class="step-by-step"]
>[Anterior](general-guidance.md) 
> [Avançar](net-framework-container-scenarios.md)
