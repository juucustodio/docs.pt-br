---
title: Microsserviços do .NET. Arquitetura de aplicativos .NET em contêineres
description: Arquitetura de microsserviços do .NET para aplicativos do .NET em contêineres | Microsserviços são serviços implantáveis de maneira modular e independente. Os contêineres do Docker (para Linux e Windows) simplificam a implantação e o teste ao agrupar um serviço e suas dependências em uma única unidade, que será executada em um ambiente isolado.
ms.date: 02/02/2021
ms.openlocfilehash: e9862445414dbe0bf9a1c5d36d790b57710028f0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99665296"
---
# <a name="net-microservices-architecture-for-containerized-net-applications"></a>Microsserviços do .NET: Arquitetura de aplicativos .NET em contêineres

![Capa do livro](./media/cover-large.png)

**Edição v 5.0** -atualizado para ASP.NET Core 5,0

Consulte o [changelog](https://aka.ms/MicroservicesEbookChangelog) para obter as atualizações do livro e as contribuições da Comunidade.

Este guia é uma introdução ao desenvolvimento de aplicativos com base em microsserviços e ao gerenciamento deles usando contêineres. Ele aborda as abordagens de design e implementação da arquitetura usando contêineres do .NET e do Docker.

Para facilitar a introdução, o guia concentra-se em um aplicativo de referência em contêineres e baseado em microsserviços que você pode explorar. O aplicativo de referência está disponível no repositório GitHub [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers).

## <a name="action-links"></a>Links de ação

- Este livro eletrônico também está disponível em um formato PDF (somente versão em inglês) [Download](https://aka.ms/microservicesebook)

- Clone/Crie fork do aplicativo de referência [eShopOnContainers no GitHub](https://github.com/dotnet-architecture/eShopOnContainers)

- Assista ao [vídeo introdutório no Channel 9](https://aka.ms/microservices-video)

- Conheça a [Arquitetura de Microsserviços](https://aka.ms/MicroservicesArchitecture) agora mesmo

## <a name="introduction"></a>Introdução

As empresas estão cada vez mais percebendo a economia de custo, resolvendo problemas de implantação e melhorando as operações de produção e de DevOps usando os contêineres. A Microsoft tem lançando inovações de contêiner para Windows e Linux com a criação de produtos como o Serviço de Kubernetes do Azure e o Azure Service Fabric e por meio de parcerias com líderes do setor como a Docker, a Mesosphere e a Kubernetes. Esses produtos oferecem soluções de contêiner que ajudam as empresas a criar e implantar aplicativos com a velocidade e a escala da nuvem, seja qual for a escolha de plataformas ou de ferramentas.

O Docker está se tornando o verdadeiro padrão no setor de contêineres, com suporte dos fornecedores mais significativos nos ecossistemas do Windows e do Linux. (A Microsoft é um dos principais fornecedores de nuvem que suportam o Docker.) No futuro, o Docker provavelmente estará onipresente em qualquer datacenter na nuvem ou no local.

Além disso, a arquitetura de [microsserviços](https://martinfowler.com/articles/microservices.html) está despontando como uma abordagem importante para aplicativos críticos distribuídos. Em uma arquitetura baseada em microsserviço, o aplicativo é criado em uma coleção de serviços que podem ser desenvolvidos, testados, implantados e ter as versões controladas de forma independente.

## <a name="about-this-guide"></a>Sobre este guia

Este guia é uma introdução ao desenvolvimento de aplicativos com base em microsserviços e ao gerenciamento deles usando contêineres. Ele aborda as abordagens de design e implementação da arquitetura usando contêineres do .NET e do Docker. Para facilitar a introdução aos contêineres e microsserviços, o guia concentra-se em um aplicativo de referência em contêineres e baseado em microsserviços que você pode explorar. O aplicativo de exemplo está disponível no repositório [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) do GitHub.

Este guia fornece o desenvolvimento básico e diretrizes arquitetônicas principalmente em um nível de ambiente de desenvolvimento com foco em duas tecnologias: Docker e .NET. Nossa intenção é que você leia este guia, ao pensar sobre o design do aplicativo sem focar a infraestrutura (nuvem ou local) do ambiente de produção. Você tomará decisões sobre a infraestrutura mais tarde, quando criar seus aplicativos prontos para produção. Portanto, este guia tem a intenção de ser independente da infraestrutura e mais centrado no ambiente de desenvolvimento.

Depois de estudar este guia, a próxima etapa será saber mais sobre os microsserviços pronto para produção no Microsoft Azure.

## <a name="version"></a>Versão

Este guia foi revisado para cobrir a versão do **.NET 5** junto com muitas atualizações adicionais relacionadas à mesma "onda" de tecnologias (isto é, Azure e tecnologias de terceiros adicionais) que coincidem no tempo com a versão do .NET 5. É por isso que a versão do livro também foi atualizada para a versão **5,0**.

## <a name="what-this-guide-does-not-cover"></a>O que este guia não cobre

Este guia não se concentra no ciclo de vida do aplicativo, em DevOps, nos pipelines de CI/CD nem no trabalho da equipe. O guia complementar [Containerized Docker Application Lifecycle with Microsoft Platform and Tools](https://aka.ms/dockerlifecycleebook) (Ciclo de vida de aplicativo do Docker em contêineres com a plataforma e as ferramentas da Microsoft) trata desse assunto. O guia atual também não fornece detalhes de implementação na infraestrutura do Azure, como informações sobre orquestradores específicos.

### <a name="additional-resources"></a>Recursos adicionais

- **Ciclo de vida do aplicativo do Docker em contêineres com a plataforma e as ferramentas da Microsoft** (livro eletrônico para download)  
    <https://aka.ms/dockerlifecycleebook>

## <a name="who-should-use-this-guide"></a>Quem deve usar este guia

Escrevemos este guia para desenvolvedores e arquitetos de solução que são novos no desenvolvimento de aplicativos com base no Docker e em arquitetura baseada em microsserviços. Este guia é para você se você quiser saber como arquitetar, projetar e implementar aplicativos de prova de conceito com tecnologias de desenvolvimento da Microsoft (com foco especial no .NET) e com contêineres do Docker.

Esse guia também será útil se você for um tomador de decisões técnicas, como um arquiteto corporativo que deseja ter uma visão geral da arquitetura e da tecnologia antes de decidir qual abordagem selecionar para aplicativos distribuídos novos e modernos.

### <a name="how-to-use-this-guide"></a>Como usar este guia

A primeira parte deste guia apresenta contêineres do Docker, discute como escolher entre o .NET 5 e o .NET Framework como uma estrutura de desenvolvimento e fornece uma visão geral dos microservices. Este conteúdo é para arquitetos e tomadores de decisões técnicas que desejam ter uma visão geral, mas que não precisam se concentrar nos detalhes da implementação de código.

A segunda parte do guia de começa com a seção [Processo de desenvolvimento de aplicativos baseados no Docker](./docker-application-development-process/index.md). Ele se concentra nos padrões de desenvolvimento e de microserviço para implementar aplicativos usando o .NET e o Docker. Esta seção será de interesse especial para desenvolvedores e arquitetos que desejam se concentrar no código, nos padrões e nos detalhes de implementação.

## <a name="related-microservice-and-container-based-reference-application-eshoponcontainers"></a>Aplicativo de referência baseado em contêiner e em microsserviço: eShopOnContainers

O aplicativo eShopOnContainers é um aplicativo de referência de código-fonte aberto para .NET e microservices que foi projetado para ser implantado usando contêineres do Docker. O aplicativo consiste em vários subsistemas, incluindo vários front-ends de interface do usuário de e-Store (um aplicativo Web MVC, um SPA da Web e um aplicativo móvel nativo). Ele também inclui os microsserviços e os contêineres de back-end de todas as operações do servidor necessárias.

A finalidade do aplicativo é demonstrar padrões de arquitetura. **A TI NÃO É UM MODELO PRONTO PARA PRODUÇÃO** para iniciar aplicativos de mundo real. Na verdade, o aplicativo está em um estado beta permanente, pois ele também é usado para testar novas tecnologias potencialmente interessantes conforme elas aparecem.

## <a name="send-us-your-feedback"></a>Envie-nos seus comentários!

Escrevemos este guia para ajudá-lo a entender a arquitetura de aplicativos em contêineres e de microsserviços no .NET. O guia e o aplicativo de referência relacionado continuarão sendo desenvolvidos, portanto seus comentários são bem-vindos! Se você tiver comentários sobre como esse guia pode ser melhorado, envie comentários em <https://aka.ms/ebookfeedback> .

## <a name="credits"></a>Credits

Coautores:

> **Cesar de la Torre**, Gerente sênior de produtos , equipe de produto do .NET, Microsoft Corp.
>
> **Bill Wagner**, Desenvolvedor sênior de conteúdo, C+E, Microsoft Corp.
>
> **Mike Rousos**, Engenheiro de Software Principal, equipe DevDiv CAT, Microsoft

Editores:

> **Mike Pope**
>
> **Steve Hoag**

Participantes e revisores:

> **Jeffrey Richter**, engenheiro de software parceiro, equipe do Azure, Microsoft
>
> **Jimmy Bogard**, Arquiteto Chefe na Headspring
>
> **Udi Dahan**, Fundador e CEO, Particular Software
>
> **Jimmy Nilsson**, Cofundador e CEO da Factor10
>
> **Glenn Condron**, Gerente sênior de programas, equipe do ASP.NET
>
> **Mark Fussell**, PM Líder Principal, equipe do Azure Service Fabric, Microsoft
>
> **Diego Vega**, PM Líder, equipe do Entity Framework, Microsoft
>
> **Barry Dorrans**, gerente de programas de segurança sênior
>
> **Rowan Miller**, Gerente sênior de programas, Microsoft
>
> **Ankit Asthana**, Gerente de PM Principal, equipe do .NET, Microsoft
>
> **Scott Hunter**, PM Diretor de Parceiro, equipe do .NET, Microsoft
>
> **Nish Anil**, Gerente de Programa Sênior, Equipe .NET, Microsoft
>
> **Dylan Reisenberger**, Arquiteto e Desenvolvedor Líder na Polly
>
> **Steve "ardalis" Smith** – Arquiteto de software e instrutor – [Ardalis.com](https://ardalis.com)
>
> **Cooper Ian**, Arquiteto de Codificação na Brighter
>
> **Unai Zorrilla**, Arquiteto e Desenvolvedor Líder na Plain Concepts
>
> **Eduard Tomas**, Desenvolvedor Líder na Plain Concepts
>
> **Ramon Tomas**, Desenvolvedor na Plain Concepts
>
> **David Sanz**, Desenvolvedor na Plain Concepts
>
> **Javier Valero**, Diretor Executivo de Operações no Grupo Solutio
>
> **Pierre Millet**, Consultor sênior, Microsoft
>
> **Michael Friis**, Gerente de Produto, Docker Inc
>
> **Charles Lowell**, Engenheiro de Software, equipe do VS CAT, Microsoft
>
> **Miguel Veloso**, engenheiro de desenvolvimento de software em conceitos simples
>
> **Pedro Ghosh**, consultor principal da Neudesic

## <a name="copyright"></a>Direitos autorais

PUBLICADO POR

Divisão de Desenvolvedores Microsoft, equipes dos produtos .NET e Visual Studio

Uma divisão da Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright © 2021 da Microsoft Corporation

Todos os direitos reservados. Nenhuma parte do conteúdo deste guia pode ser reproduzida ou transmitida de nenhuma forma nem por nenhum meio sem a permissão por escrito do publicador.

Este livro é fornecido “no estado em que se encontra” e expressa os pontos de vista e as opiniões do autor. Os pontos de vista, as opiniões e as informações expressos neste guia, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.

 Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios. Nenhuma associação ou conexão real é intencional ou deve ser inferida.

A Microsoft e as marcas listadas em <https://www.microsoft.com> na página da Web "Marcas" são marcas comerciais do grupo de empresas Microsoft.

Mac e macOS são marcas comerciais da Apple Inc.

O logotipo de redistribuição do Docker é uma marca registrada do Docker, Inc. usada pela permissão.

Todas as outras marcas e logotipos são propriedade de seus respectivos proprietários.

>[!div class="step-by-step"]
>[Próximo](container-docker-introduction/index.md)
