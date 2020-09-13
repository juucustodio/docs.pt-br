---
title: Visão geral de tutoriais passo a passo e introduções técnicas
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Visão geral de orientações técnicas e de introdução técnica
ms.date: 04/28/2018
ms.openlocfilehash: 4db6d449d27dcd4316d61305c8c2a8c2aa0bc65b
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516119"
---
# <a name="walkthroughs-and-technical-get-started-overview"></a>Visão geral de tutoriais passo a passo e introduções técnicas

Para limitar o tamanho deste livro eletrônico, documentação técnica adicional e os passo a passos completos foram disponibilizados em um repositório GitHub. A série online de instruções explicativas descritas neste capítulo aborda a configuração passo a passo dos vários ambientes baseados em contêineres do Windows e a implantação no Azure.

As seções a seguir explicam o que envolve cada explicação, seus objetivos e visão de alto nível e fornece um diagrama das tarefas envolvidas. Você pode obter os passo a passos em si no wiki do repositório GitHub de aplicativos *eShopModernizing* em <https://github.com/dotnet-architecture/eShopModernizing/wiki> .

## <a name="technical-walkthrough-list"></a>Lista de instruções técnicas

Os seguintes passo a passos de introdução fornecem diretrizes técnicas consistentes e abrangentes para aplicativos de exemplo que podem ser movidos e deslocados usando contêineres e, em seguida, se movem usando várias opções de implantação no Azure.

Cada uma das orientações a seguir usa os novos aplicativos de exemplo eShopLegacy e eShopModernizing, que estão disponíveis no GitHub em <https://github.com/dotnet-architecture/eShopModernizing> .

- **Tour dos aplicativos herdados eShop (aplicativos de linha de base para modernizar)**

- **Colocar em contêineres seus aplicativos Web ASP.NET existentes (WebForms & MVC) com contêineres do Windows**

- **Colocar em contêineres seus serviços WCF existentes (aplicativos de N camadas) com contêineres do Windows**

- **Implantar seu aplicativo baseado em contêineres do Windows em VMs do Azure**

- **Implantar seus aplicativos baseados em contêineres do Windows no kubernetes no serviço de contêiner do Azure**

## <a name="walkthrough-1-tour-of-eshop-legacy-apps"></a>Walkthrough 1: Tour dos aplicativos herdados do eShop

### <a name="technical-walkthrough-availability"></a>Disponibilidade de instruções técnicas

A explicação técnica completa está disponível no wiki do repositório GitHub do eShopModernizing:

[passo a passos do eShopModernizing wiki](https://github.com/dotnet-architecture/eShopModernizing/wiki)

### <a name="overview"></a>Visão geral

Neste tutorial, você pode explorar a implementação inicial de três aplicativos herdados de exemplo. Os dois primeiros aplicativos Web de exemplo têm uma arquitetura monolítica e foram criados usando ASP.NET clássicas. Um aplicativo é baseado em ASP.NET 4. x MVC; o segundo aplicativo é baseado em Web Forms ASP.NET 4. x.
O terceiro aplicativo é um aplicativo de três camadas composto por um aplicativo WinForms cliente e um serviço de Windows Communication Foundation do lado do servidor [(WCF)](../../framework/wcf/whats-wcf.md) .

Todos esses aplicativos estão disponíveis no [repositório GitHub do eShopModernizing](https://github.com/dotnet-architecture/eShopModernizing).

### <a name="goals"></a>Metas

A principal meta deste passo a passo é simplesmente se familiarizar com esses aplicativos e com seu código e configuração. Você pode configurar os aplicativos para que eles gerem e usem dados fictícios, sem usar o banco de dado SQL, para fins de teste. Essa configuração opcional é baseada na injeção de dependência, de forma desacoplada.

### <a name="scenario-1-aspnet-web-apps"></a>Cenário 1: aplicativos Web ASP.NET

A figura a seguir mostra o cenário simples dos aplicativos Web ASP.NET herdados originais.

![Cenário de arquitetura simples dos aplicativos Web ASP.NET herdados originais](./media/image5-1.png)

De uma perspectiva de domínio de negócios, ambos os aplicativos oferecem os mesmos recursos de gerenciamento de catálogo. Os membros da equipe do eShop Enterprise usariam o aplicativo para exibir e editar o catálogo de produtos.

A próxima figura mostra as capturas de tela iniciais do aplicativo.

![ASP.NET MVC e ASP.NET Web Forms aplicativos (tecnologias existentes/herdadas)](./media/image5-2.png)

Dependências no ASP.NET 4. x ou versões anteriores (para MVC ou para Web Forms) significa que esses aplicativos não serão executados no .NET Core, a menos que o código seja totalmente reescrito usando ASP.NET Core MVC.

### <a name="scenario-2-wcf-service-and-winforms-client-app-3-tier-app"></a>Cenário 2: serviço WCF e aplicativo cliente WinForms (aplicativo de três camadas)

A figura a seguir mostra o cenário simples do aplicativo herdado de três camadas original.

![Cenário de arquitetura simples do aplicativo de três camadas herdado original com um serviço WCF e um aplicativo cliente WinForms](./media/image5-1.5.png)

### <a name="benefits"></a>Benefícios

Os benefícios deste passo a passos são simples: Familiarize-se apenas com o código e os aplicativos iniciais.

### <a name="next-steps"></a>Próximas etapas

Explore este conteúdo mais detalhadamente no wiki do GitHub:

- [Tour na linha de base ASP.NET MVC e Web Forms aplicativos "herdados"](https://github.com/dotnet-architecture/eShopModernizing/wiki/01.-Tour-on-the-ASP.NET-MVC-and-WebForms-apps-implementation-code)
- [Tour no serviço WCF de linha de base e no aplicativo WinForms (3 camadas) "herdado"](https://github.com/dotnet-architecture/eShopModernizing/wiki/21.-Tour-on-the-WCF-service-and-WinForms-apps)

## <a name="walkthrough-2-containerize-your-existing-net-applications-with-windows-containers"></a>Walkthrough 2: colocar seus aplicativos .NET em contêineres existentes com contêineres do Windows

### <a name="overview"></a>Visão geral

Use contêineres do Windows para aprimorar a implantação de aplicativos .NET existentes, como aqueles baseados em MVC, Web Forms ou WCF, para ambientes de produção, desenvolvimento e teste.

### <a name="goals"></a>Metas

O objetivo deste passo a passo é mostrar várias opções para o contêiner de um aplicativo .NET Framework existente. Você pode:

- Colocar seu aplicativo em contêiner usando as [Ferramentas do visual studio 2017 para Docker](/aspnet/core/host-and-deploy/docker/visual-studio-tools-for-docker) (visual Studio 2017 ou versões posteriores).

- Colocar seu aplicativo em contêiner Adicionando manualmente um [Dockerfile](https://docs.docker.com/engine/reference/builder/)e, em seguida, usando a [CLI do Docker](https://docs.docker.com/engine/reference/commandline/cli/).

- Colocar seu aplicativo em contêiner usando a ferramenta [Img2Docker](https://github.com/docker/communitytools-image2docker-win) (uma ferramenta de código-fonte aberto do Docker).

Este tutorial explica a abordagem das ferramentas do Visual Studio 2017 para Docker, mas as outras duas abordagens são bastante semelhantes em relação ao uso de Dockerfiles.

### <a name="scenario-1-containerized-aspnet-web-apps"></a>Cenário 1: aplicativos Web ASP.NET em contêineres

A figura abaixo mostra o cenário para aplicativos de aplicativos Web herdados do eShop em contêineres.

![Diagrama de arquitetura simplificado de aplicativos ASP.NET em contêineres em um ambiente de desenvolvimento](./media/image5-3.png)

### <a name="scenario-2-containerized-wcf-service"></a>Cenário 2: serviço WCF em contêineres

A figura abaixo mostra o cenário para um aplicativo de três camadas com um serviço WCF em contêiner.

![Diagrama de arquitetura simplificado do serviço WCF em contêineres em um ambiente de desenvolvimento](./media/image5-3.5.png)

### <a name="benefits"></a>Benefícios

Há vantagens em executar seu aplicativo monolítico em um contêiner. Primeiro, você cria uma imagem para o aplicativo. Desse ponto em diante, cada implantação é executada no mesmo ambiente. Cada contêiner usa a mesma versão do sistema operacional, tem a mesma versão das dependências instaladas, usa a mesma versão do .NET Framework e é criado usando o mesmo processo. Basicamente, você controla as dependências do seu aplicativo usando uma imagem do Docker. As dependências viajam com o aplicativo quando você implanta os contêineres.

Um benefício adicional é que os desenvolvedores podem executar o aplicativo no ambiente consistente fornecido pelos contêineres do Windows. Os problemas que aparecem apenas com determinadas versões podem ser exibidos imediatamente, em vez de identificando em um ambiente de preparo ou de produção. As diferenças em ambientes de desenvolvimento usados por membros da equipe de desenvolvimento importam menos quando os aplicativos são executados em contêineres.

Os aplicativos em contêineres também têm uma curva de expansão Flatter. Os aplicativos em contêineres permitem que você tenha mais instâncias de aplicativo e de serviço (com base em contêineres) em uma VM ou máquina física em comparação com implantações regulares de aplicativos por máquina. Isso se traduz em maior densidade e menos recursos necessários, especialmente quando você usa orquestradores como kubernetes.

A criação de contêineres, nas situações ideais, não requer nenhuma alteração no código do aplicativo (C \# ). Na maioria dos cenários, você só precisa dos arquivos de metadados de implantação do Docker (arquivos Dockerfiles e Docker Compose).

### <a name="next-steps"></a>Próximas etapas

Explore este conteúdo mais detalhadamente no wiki do GitHub:

- [Como colocar o .NET Framework aplicativos Web em contêineres com contêineres do Windows e Docker](https://github.com/dotnet-architecture/eShopModernizing/wiki/02.-How-to-containerize-the-.NET-Framework-web-apps-with-Windows-Containers-and-Docker)
- [Adicionando suporte ao Docker a um serviço WCF](https://github.com/dotnet-architecture/eShopModernizing/wiki/22.-Adding-Docker-Support)

## <a name="walkthrough-3-deploy-your-windows-containers-based-app-to-azure-vms"></a>Walkthrough 3: implantar seu aplicativo baseado em contêineres do Windows para VMs do Azure

### <a name="technical-walkthrough-availability"></a>Disponibilidade de instruções técnicas

A explicação técnica completa está disponível no wiki do repositório GitHub do eShopModernizing: <https://github.com/dotnet-architecture/eShopModernizing/wiki/06.-Deploying-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)>

### <a name="overview"></a>Visão geral

A implantação em um host do Docker em uma VM (máquina virtual) do Windows Server 2016 no Azure permite que você configure rapidamente ambientes de desenvolvimento/teste/preparo. Ele também oferece um lugar comum para os testadores ou usuários empresariais validarem o aplicativo. As VMs também podem ser ambientes de produção de IaaS (infraestrutura como serviço) válidos.

### <a name="goals"></a>Metas

O objetivo deste passo a passo é mostrar as várias alternativas que você tem ao implantar contêineres do Windows em VMs do Azure baseadas no Windows Server 2016 ou versões posteriores.

### <a name="scenarios"></a>Cenários

Vários cenários são abordados neste passo a passos.

#### <a name="scenario-a-deploy-to-an-azure-vm-from-a-dev-pc-through-docker-engine-connection"></a>Cenário A: implantar em uma VM do Azure de um PC de desenvolvimento por meio da conexão do mecanismo do Docker

![Implantar em uma VM do Azure de um PC de desenvolvimento por meio de uma conexão de mecanismo do Docker](./media/image5-4.png)

**Figura 5-4.** Implantar em uma VM do Azure de um PC de desenvolvimento por meio de uma conexão de mecanismo do Docker

#### <a name="scenario-b-deploy-to-an-azure-vm-through-a-docker-registry"></a>Cenário B: implantar em uma VM do Azure por meio de um registro do Docker

![Implantar em uma VM do Azure por meio de um registro do Docker](./media/image5-5.png)

**Figura 5-5.** Implantar em uma VM do Azure por meio de um registro do Docker

#### <a name="scenario-c-deploy-to-an-azure-vm-from-cicd-pipelines-in-azure-devops-services"></a>Cenário C: implantar em uma VM do Azure de pipelines de CI/CD no Azure DevOps Services

![Implantar em uma VM do Azure de pipelines de CI/CD no Azure DevOps Services](./media/image5-6.png)

**Figura 5-6.** Implantar em uma VM do Azure de pipelines de CI/CD no Azure DevOps Services

### <a name="azure-vms-for-windows-containers"></a>VMs do Azure para contêineres do Windows

As VMs do Azure para contêineres do Windows são VMs baseadas no Windows Server 2016, Windows 10 ou versões posteriores, com o mecanismo do Docker configurado. Na maioria dos casos, o Windows Server 2016 é usado nas VMs do Azure.

Atualmente, o Azure fornece uma VM chamada **Windows Server 2016 com contêineres**. Você pode usar essa VM para experimentar o novo recurso de contêiner do Windows Server, com o Windows Server Core ou o Windows nano Server. As imagens do sistema operacional do contêiner são instaladas e, em seguida, a VM está pronta para ser usada com o Docker.

### <a name="benefits"></a>Benefícios

Embora os contêineres do Windows possam ser implantados em VMs do Windows Server 2016 locais, quando você implanta no Azure, você obtém uma maneira mais fácil de começar, com VMs de contêiner do Windows Server prontas para uso. Você também obtém um local online comum que é acessível aos testadores e escalabilidade automática por meio de conjuntos de dimensionamento de máquinas virtuais do Azure.

### <a name="next-steps"></a>Próximas etapas

Explore este conteúdo mais detalhadamente no wiki do GitHub:

<https://github.com/dotnet-architecture/eShopModernizing/wiki/06.-Deploying-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)>

## <a name="walkthrough-4-deploy-your-windows-containers-based-apps-to-azure-container-instances-aci"></a>Walkthrough 4: implantar seus aplicativos baseados em contêineres do Windows em ACI (instâncias de contêiner do Azure)

### <a name="technical-walkthrough-availability"></a>Disponibilidade de instruções técnicas

A explicação técnica completa está disponível no wiki do repositório GitHub do eShopModernizing:

[Implantando os aplicativos no ACI (instâncias de contêiner do Azure)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances))

### <a name="overview"></a>Visão geral

[ACI (instâncias de contêiner do Azure)](https://docs.microsoft.com/azure/container-instances/) é a maneira mais rápida de ter um ambiente de desenvolvimento/teste/preparo de contêineres no qual você pode implantar instâncias únicas de contêineres.

### <a name="goals"></a>Metas

Este passo a passos mostra os principais cenários ao implantar contêineres do Windows em ACI (instâncias de contêiner do Azure) e como você pode implantar aplicativos eShopModernizing no ACI.

### <a name="scenarios"></a>Cenários

Pode haver variações sobre a implantação de aplicativos eShopModernizing em ACI, como a implantação de apenas um ou todos os aplicativos (aplicativo MVC, aplicativo WebForms ou serviço WCF). No cenário a seguir mostrado abaixo, você pode ver o aplicativo ASP.NET MVC mais o contêiner SQL Server ambos implantados como contêineres em ACI (instâncias de contêiner do Azure).

![Implantar no ACI de um ambiente de desenvolvimento](./media/image5-3.5.6.png)

### <a name="benefits"></a>Benefícios

As Instâncias de Contêiner do Azure facilitam criar e gerenciar contêineres do Docker no Azure, sem a necessidade de provisionar máquinas virtuais ou adotar um serviço de nível superior. Com o ACI, você pode implantar diretamente um contêiner do Windows no Azure e expô-lo à Internet com um FQDN (nome de domínio totalmente qualificado) em questão de segundos (desde que você tenha a imagem de contêiner do Windows pronta em um registro do Docker, como o Hub do Docker ou o registro de contêiner do Azure).

### <a name="considerations"></a>Considerações

A implantação de contêineres do Windows com total .NET Framework/ASP.NET ou SQL Server nas instâncias de contêiner do Azure (ACI) não é tão rápida quanto a implantação em um host do Docker regular (como um Windows Server 2016 com contêineres do Windows) porque a imagem do Docker precisa ser baixada (extraída do registro do Docker) toda vez e os tamanhos de a imagem de contêiner SQL (15,1 GB) e a imagem de contêiner ASP.NET (13,9 GB) são significativamente grandes, no entanto, é muito mais barato do que manter seu próprio host do Docker (permanentemente online o Windows Server 2016 com a VM de contêineres do Windows no Azure) para não mencionar um orquestrador inteiro como kubernetes no Azure (AKS), que é, por outro lado, uma ótima opção para implantações de produção.

Como conclusão principal, o uso de instâncias de contêiner do Azure é uma opção muito atraente para cenários de desenvolvimento/teste e para pipelines de CI/CD.

### <a name="next-steps"></a>Próximas etapas

Explore este conteúdo mais detalhadamente no wiki do GitHub:

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances))

## <a name="walkthrough-5-deploy-your-windows-containers-based-apps-to-kubernetes-in-azure-container-service"></a>Walkthrough 5: implantar seus aplicativos baseados em contêineres do Windows no kubernetes no serviço de contêiner do Azure

### <a name="technical-walkthrough-availability"></a>Disponibilidade de instruções técnicas

A explicação técnica completa está disponível no wiki do repositório GitHub do eShopModernizing:

<https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

### <a name="overview"></a>Visão geral

Um aplicativo baseado em contêineres do Windows precisará usar rapidamente as plataformas, movendo-se ainda mais longe das VMs IaaS. Isso é necessário para obter alta escalabilidade e melhor escalabilidade automatizada, e para uma melhoria significativa em implantações e versões automatizadas. Você pode atingir essas metas usando o Orchestrator [kubernetes](https://kubernetes.io/), disponível nos [serviços de contêiner do Azure](https://azure.microsoft.com/services/container-service/).

### <a name="goals"></a>Metas

O objetivo deste passo a passo é aprender como implantar um aplicativo baseado em contêiner do Windows para kubernetes (também chamado de *K8s*) no serviço de contêiner do Azure. A implantação do kubernetes do zero é um processo de duas etapas:

1. Implante um cluster kubernetes no serviço de contêiner do Azure.

2. Implante o aplicativo e os recursos relacionados ao cluster kubernetes.

### <a name="scenarios"></a>Cenários

#### <a name="scenario-a-deploy-directly-to-a-kubernetes-cluster-from-a-dev-environment"></a>Cenário A: implantar diretamente em um cluster kubernetes de um ambiente de desenvolvimento

![Implantar diretamente em um cluster kubernetes de um ambiente de desenvolvimento](./media/image5-7.png)

**Figura 5-7.** Implantar diretamente em um cluster kubernetes de um ambiente de desenvolvimento

#### <a name="scenario-b-deploy-to-a-kubernetes-cluster-from-cicd-pipelines-in-azure-devops-services"></a>Cenário B: implantar em um cluster kubernetes de pipelines de CI/CD no Azure DevOps Services

![Implantar em um cluster kubernetes de pipelines de CI/CD no Azure DevOps Services](./media/image5-8.png)

**Figura 5-8.** Implantar em um cluster kubernetes de pipelines de CI/CD no Azure DevOps Services

### <a name="benefits"></a>Benefícios

Há muitos benefícios em implantar em um cluster no kubernetes. A maior vantagem é que você obtém um ambiente pronto para produção no qual pode escalar horizontalmente o aplicativo com base no número de instâncias de contêiner que deseja usar (escalabilidade interna nos nós existentes) e com base no número de nós ou VMs no cluster (escalabilidade global do cluster).

O serviço de contêiner do Azure otimiza ferramentas e tecnologias populares de software livre especificamente para o Azure. Você Obtém uma solução aberta que oferece portabilidade, tanto para seus contêineres quanto para a configuração do aplicativo. Você seleciona o tamanho, o número de hosts e o serviço de contêiner de ferramentas do Orchestrator lida com todo o resto.

Com o kubernetes, os desenvolvedores podem progredir de pensar em máquinas virtuais e físicas, planejar uma infraestrutura centrada em contêineres que facilite os seguintes recursos, entre outros:

- Aplicativos baseados em vários contêineres

- Replicando instâncias de contêiner e dimensionamento automático horizontal

- Nomenclatura e descoberta (por exemplo, DNS interno)

- Cargas de balanceamento

- Atualizações sem interrupção

- Distribuindo segredos

- Verificações de integridade do aplicativo

### <a name="next-steps"></a>Próximas etapas

Explore este conteúdo mais detalhadamente no wiki do GitHub: <https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

## <a name="walkthrough-6-deploy-your-windows-containers-based-apps-to-azure-app-service-for-containers"></a>Walkthrough 6: implantar seus aplicativos baseados em contêineres do Windows para Azure App serviço para contêineres

### <a name="technical-walkthrough-availability"></a>Disponibilidade de instruções técnicas

A explicação técnica completa está disponível no wiki do repositório GitHub do eShopModernizing:

<https://github.com/dotnet-architecture/eShopModernizing/wiki/Deploy-Windows-Container-to-Azure-App-Service>

### <a name="overview"></a>Visão geral

Um aplicativo em contêineres simples usando contêineres do Windows pode ser facilmente implantado para Azure App serviço para contêineres. Essa é a abordagem recomendada para a maioria dos aplicativos baseados em contêiner do Windows.

### <a name="goals"></a>Metas

O objetivo deste passo a passo é aprender como implantar um aplicativo baseado em contêiner do Windows para Azure App serviço para contêineres de um registro (Hub do Docker ou registro de contêiner do Azure).

### <a name="scenario"></a>Cenário

![Implantar o aplicativo baseado em contêiner do Windows no serviço Azure App para contêineres](./media/image5-11.png)

### <a name="benefits"></a>Benefícios

A implantação no serviço de Azure App para contêineres oferece os benefícios dos contêineres emparelhados com os benefícios de PaaS do serviço Azure App. O serviço de aplicativo pode ser facilmente dimensionado vertical e horizontalmente e pode ser configurado para dimensionamento automático para atender às demandas em constante mudança. As atualizações podem ser executadas com zero tempo de inatividade e a configuração da implantação contínua de um registro também é facilmente configurada.

### <a name="next-steps"></a>Próximas etapas

Explore este conteúdo mais detalhadamente no wiki do GitHub: <https://github.com/dotnet-architecture/eShopModernizing/wiki/Deploy-Windows-Container-to-Azure-App-Service>

> [!div class="step-by-step"]
> [Anterior](modernize-existing-apps-to-cloud-optimized/migrate-to-hybrid-cloud-scenarios.md) 
>  [Avançar](conclusions.md) <!-- Next Chapter -->
