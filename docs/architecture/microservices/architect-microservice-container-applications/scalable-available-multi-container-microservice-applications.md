---
title: Orquestrar microsserviços e aplicativos de vários contêineres para alta escalabilidade e disponibilidade
description: Descubra as opções para orquestrar microsserviços e aplicativos de vários contêineres para alta escalabilidade e disponibilidade e as possibilidades de Azure Dev Spaces durante o desenvolvimento do ciclo de vida de aplicativos Kubernetes.
ms.date: 01/13/2021
ms.openlocfilehash: 7ba0367bca98edbab1be2059ee37e863359edad3
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189402"
---
# <a name="orchestrate-microservices-and-multi-container-applications-for-high-scalability-and-availability"></a>Orquestrar microsserviços e aplicativos de vários contêineres para alta escalabilidade e disponibilidade

O uso de orquestradores em aplicativos prontos para produção é essencial se o aplicativo for baseado em microsserviços ou simplesmente dividido em vários contêineres. Conforme apresentado anteriormente, em uma abordagem baseada em microsserviço, cada microsserviço tem seu próprio modelo e dados para que seja autônomo de um ponto de vista de desenvolvimento e implantação. No entanto, se o aplicativo for mais tradicional, composto por diversos serviços (como o SOA), também haverá vários contêineres ou serviços que abrangem um único aplicativo de negócios e precisam ser implantados como um sistema distribuído. Esses tipos de sistemas são difíceis de escalar horizontalmente e gerenciar; portanto, um orquestrador é absolutamente necessário para ter um aplicativo pronto para produção, escalonável e com vários contêineres.

A Figura 4-23 ilustra a implantação de um aplicativo composto por vários microsserviços (contêineres) em um cluster.

![Diagrama mostrando os aplicativos do Docker compostos em um cluster.](./media/scalable-available-multi-container-microservice-applications/composed-docker-applications-cluster.png)

**Figura 4-23**. Um cluster de contêineres

você pode usar um contêiner para cada instância de serviço. Os contêineres do Docker são "unidades de implantação" e um contêiner é uma instância de um Docker. Um host lida com muitos contêineres. Parece ser uma abordagem lógica. Mas como você lida com o balanceamento de carga, roteamento e orquestração desses aplicativos compostos?

O Docker Engine simples em hosts individuais do Docker atende às necessidades de gerenciamento de instâncias de imagem única em um host, mas fica aquém quando se trata de gerenciar vários contêineres implantados em diversos hosts de aplicativos distribuídos mais complexos. Na maioria dos casos, você precisa de uma plataforma de gerenciamento que iniciará automaticamente os contêineres, expandir contêineres com várias instâncias por imagem, suspendá-los ou desligá-los quando necessário e, idealmente, controlar como eles acessam recursos como a rede e o armazenamento de dados.

Para ir além do gerenciamento de contêineres individuais ou aplicativos compostos simples e em direção a aplicativos empresariais com microsserviços, é necessário adotar a orquestração e as plataformas de clustering.

De uma perspectiva de arquitetura e desenvolvimento, ao criar aplicativos empresariais grandes, compostos e baseados em microsserviços, é importante entender as seguintes plataformas e produtos que dão suporte a cenários avançados:

**Clusters e orquestradores.** Quando é preciso expandir os aplicativos em vários hosts do Docker, como um aplicativo grande baseado em microsserviço, é essencial ter a capacidade de gerenciar todos esses hosts como um cluster único, abstraindo a complexidade da plataforma subjacente. É isso que os clusters e orquestradores de contêineres fazem. O Kubernetes é um exemplo de orquestrador e está disponível no Azure por meio do Serviço de Kubernetes do Azure.

**Agendadores.** *Agendamento* é a capacidade do administrador de iniciar contêineres em um cluster para que eles também forneçam uma interface do usuário. O agendador do cluster tem diversas responsabilidades: usar os recursos de cluster de forma eficiente, definir as restrições fornecidas pelo usuário, balancear a carga dos contêineres em nós ou hosts de maneira eficaz, ser robusto contra erros e, ao mesmo tempo, oferecer alta disponibilidade.

Os conceitos de "cluster" e "agendador" estão intimamente relacionados, então os produtos oferecidos por diferentes fornecedores geralmente têm as duas capacidades. A lista a seguir mostra a plataforma mais importante e opções de software para clusters e agendadores. Geralmente, esses orquestradores são oferecidos em nuvens públicas como o Azure.

## <a name="software-platforms-for-container-clustering-orchestration-and-scheduling"></a>Plataformas de software para clustering, orquestração e agendamento de contêineres

|     |   |
|:---:|---|
| **Kubernetes** <br> ![Uma imagem do logotipo do kubernetes.](./media/scalable-available-multi-container-microservice-applications/kubernetes-container-orchestration-system-logo.png) | O [*Kubernetes*](https://kubernetes.io/) é um produto de software livre que oferece funcionalidades que variam da infraestrutura do cluster e do agendamento de contêiner a capacidades de orquestração. Com ele, é possível automatizar a implantação, o escalonamento e as operações de contêineres de aplicativo em clusters de hosts. <br><br> O *Kubernetes* oferece uma infraestrutura centrada no contêiner que agrupa contêineres de aplicativo em unidades lógicas para facilitar o gerenciamento e a descoberta. <br><br> O *Kubernetes* é maduro no Linux e menos maduro no Windows. |
| **AKS (Serviço de Kubernetes do Azure)** <br> ![Uma imagem do logotipo do serviço kubernetes do Azure.](./media/scalable-available-multi-container-microservice-applications/azure-kubernetes-service-logo.png) | O [AKs](https://azure.microsoft.com/services/kubernetes-service/) é um serviço de orquestração de contêiner kubernetes gerenciado no Azure que simplifica o gerenciamento, a implantação e as operações do cluster kubernetes. |

## <a name="using-container-based-orchestrators-in-microsoft-azure"></a>Usar orquestradores baseados em contêiner no Microsoft Azure

Diversos provedores de nuvem oferecem suporte a contêineres do Docker e seus clusters e orquestração, como o Microsoft Azure, o Amazon EC2 Container Service e o Google Container Engine. O Microsoft Azure fornece suporte ao orquestrador e ao cluster do Docker por meio do AKS (Serviço de Kubernetes do Azure).

## <a name="using-azure-kubernetes-service"></a>Usando o Serviço de Kubernetes do Azure

Um cluster do Kubernetes cria um pool de diversos hosts do Docker e os expõe como um host virtual único. Assim, é possível implantar vários contêineres no cluster e expandir com qualquer número de instâncias de contêiner. O cluster lidará com todos os detalhes complexos de gerenciamento, como escalabilidade, integridade e assim por diante.

O AKS é uma maneira de simplificar a criação, configuração e gerenciamento de um cluster de máquinas virtuais no Azure pré-configuradas para executar aplicativos em contêineres. Ao utilizar uma configuração otimizada de ferramentas de software livre conhecidas de agendamento e orquestração, o AKS permite o uso de habilidades existentes ou recorre ao grande e crescente conhecimento da comunidade para implantar e gerenciar aplicativos baseados em contêiner no Microsoft Azure.

O Serviço de Kubernetes do Azure otimiza a configuração de ferramentas de software livre e tecnologias conhecidas do Docker especificamente para o Azure. É uma solução aberta que oferece portabilidade para contêineres e configuração de aplicativo. Selecione o tamanho, a quantidade de hosts e as ferramentas de orquestrador e deixe o AKS cuidar de todo o resto.

![Diagrama mostrando uma estrutura de cluster kubernetes.](./media/scalable-available-multi-container-microservice-applications/kubernetes-cluster-simplified-structure.png)

**Figura 4-24**. Topologia e estrutura simplificadas do cluster Kubernetes

Na Figura 4-24, você pode ver a estrutura de um cluster kubernetes em que um nó mestre (VM) controla a maior parte da coordenação do cluster e você pode implantar contêineres no restante dos nós, que são gerenciados como um único pool de um ponto de vista de aplicativo e permitem que você dimensione para milhares ou até mesmo dezenas de milhares de contêineres.

## <a name="development-environment-for-kubernetes"></a>Ambiente de desenvolvimento para Kubernetes

No ambiente de desenvolvimento, o [Docker anunciou em julho de 2018](https://blog.docker.com/2018/07/kubernetes-is-now-available-in-docker-desktop-stable-channel/) que o kubernetes também pode ser executado em uma única máquina de desenvolvimento (Windows 10 ou MacOS) instalando o [Docker desktop](https://docs.docker.com/install/). Posteriormente, você pode implantar para a nuvem (AKS) para testes de integração posteriores, conforme mostrado na figura 4-25.

![Diagrama mostrando kubernetes em um computador de desenvolvimento, então implantado no AKS](./media/scalable-available-multi-container-microservice-applications/kubernetes-development-environment.png)

**Figura 4-25**. Executando Kubernetes no computador de desenvolvimento e na nuvem

## <a name="getting-started-with-azure-kubernetes-service-aks"></a>Introdução ao AKS (Serviço de Kubernetes do Azure)

Para começar a usar o AKS, implante um cluster do AKS do portal do Azure ou usando a CLI. Para saber mais sobre como implantar um cluster do Kubernetes no Azure, veja [Implantar um cluster do AKS (Serviço de Kubernetes do Azure)](/azure/aks/kubernetes-walkthrough-portal).

Nenhum valor é cobrado pelos softwares instalados por padrão como parte do AKS. Todas as opções padrão são implementadas com software livre. O AKS está disponível para várias máquinas virtuais no Azure. Você é cobrado apenas pelas instâncias de computação que escolher e os outros recursos de infraestrutura subjacente consumidos, como armazenamento e rede. Não há cobranças adicionais pelo AKS.

A opção de implantação de produção padrão para kubernetes é usar gráficos Helm, que são introduzidos na próxima seção.

## <a name="deploy-with-helm-charts-into-kubernetes-clusters"></a>Implantar com gráficos do Helm em clusters Kubernetes

Ao implantar um aplicativo em um cluster Kubernetes, você pode usar a ferramenta de CLI kubectl.exe original usando arquivos de implantação com base no formato nativo (arquivos .yaml), conforme já mencionado na seção anterior. No entanto, para aplicativos mais complexos do Kubernetes, como ao implantar aplicativos complexos baseados em microsserviços, é recomendável usar o [Helm](https://helm.sh/).

Os Gráficos do Helm ajudam você a definir, realizar controle de versão, instalar, compartilhar, atualizar ou reverter até mesmo o aplicativo mais complexo do Kubernetes.

Indo além, o uso de Helm também é recomendado porque outros ambientes de kubernetes no Azure, como [Azure dev Spaces](/azure/dev-spaces/azure-dev-spaces) também são baseados em gráficos de Helm.

O Helm é mantido pela [CNCF (nuvem Native Computing Foundation)](https://www.cncf.io/) – em colaboração com a Microsoft, o Google, o BitNami e a comunidade de colaboradores do Helm.

Para obter mais informações de implementação sobre gráficos Helm e kubernetes, consulte o [usando gráficos do Helm para implantar eShopOnContainers em AKs](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Deploy-to-Azure-Kubernetes-Service-(AKS)) post.

## <a name="use-azure-dev-spaces-for-your-kubernetes-application-lifecycle"></a>Usar o Azure Dev Spaces para o ciclo de vida do aplicativo do Kubernetes

[Azure dev Spaces](/azure/dev-spaces/azure-dev-spaces) fornece uma experiência de desenvolvimento kubernetes rápida e iterativa para equipes. Com algumas poucas configurações de máquina de desenvolvimento, você pode executar e depurar contêineres de forma iterativa diretamente no Azure Kubernetes Service (AKS). Desenvolva no Windows, Mac ou Linux usando ferramentas familiares como o Visual Studio, Visual Studio Code ou a linha de comando.

Conforme mencionado, o Azure Dev Spaces usa gráficos do Helm ao implantar os aplicativos baseados em contêiner.

Azure Dev Spaces ajuda as equipes de desenvolvimento a serem mais produtivas no kubernetes porque ela permite que você itere e depure rapidamente o código diretamente em um cluster kubernetes global no Azure usando o Visual Studio 2019 ou o Visual Studio Code. Esse cluster Kubernetes no Azure é um cluster Kubernetes gerenciado compartilhado, de modo que sua equipe pode trabalhar conjuntamente de forma colaborativa. Você pode desenvolver o código de forma isolada, depois implantar no cluster global e realizar testes de ponta a ponta com outros componentes sem replicar ou criar dependências fictícias.

Conforme mostrado na Figura 4-26, o recurso mais diferencial no Azure Dev Spaces é a capacidade de criar "espaços" que podem ser executados integrados ao restante da implantação global no cluster.

![Diagrama mostrando o uso de vários espaços em Azure Dev Spaces.](./media/scalable-available-multi-container-microservice-applications/use-multiple-spaces-azure-dev.png)

**Figura 4-26**. Usando vários espaços no Azure Dev Spaces

Basicamente, você pode configurar um espaço de desenvolvimento compartilhado no Azure. Cada desenvolvedor pode se concentrar apenas em sua parte do aplicativo e pode desenvolver iterativamente um código de pré-confirmação em um espaço de desenvolvimento que já contém todos os outros serviços e recursos de nuvem dos quais seus cenários dependem. As dependências estão sempre atualizadas, e os desenvolvedores trabalham de uma forma que reflete a produção.

O Azure Dev Spaces oferece o conceito de um espaço, que permite trabalhar em relativo isolamento e sem medo de interromper o trabalho da equipe. Cada espaço de desenvolvimento faz parte de uma estrutura hierárquica que permite que você substitua um ou muitos microsserviços a partir do espaço de desenvolvimento mestre “top” com seu próprio microsserviço em andamento.

Esse recurso se baseia nos prefixos de URL, portanto, ao usar qualquer prefixo de espaço de desenvolvimento na URL, uma solicitação é enviada do microsserviço de destino caso ele exista no espaço de desenvolvimento; caso contrário, ela é encaminhada até a primeira instância do microsserviço de destino encontrado na hierarquia, chegando ao espaço de desenvolvimento mestre na parte superior em algum momento.

Para obter uma exibição prática em um exemplo concreto, consulte a [página wiki do eShopOnContainers em Azure dev Spaces](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Azure-Dev-Spaces).

Para obter mais informações, consulte o artigo sobre [desenvolvimento de equipe com Azure dev Spaces](/azure/dev-spaces/team-development-netcore).

## <a name="additional-resources"></a>Recursos adicionais

- **Introdução ao serviço kubernetes do Azure (AKS)** \
  <https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal>

- **Azure Dev Spaces** \
  <https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces>

- **Kubernetes** O site oficial. \
  <https://kubernetes.io/>

>[!div class="step-by-step"]
>[Anterior](resilient-high-availability-microservices.md) 
> [Avançar](../docker-application-development-process/index.md)
