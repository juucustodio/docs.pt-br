---
title: Outras opções de implantação de contêiner
description: Outras opções de implantação de contêiner usando o Azure
ms.date: 05/13/2020
ms.openlocfilehash: 2eac822b74af636e0ab0ed24b58eb7139526f4a2
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91163616"
---
# <a name="other-container-deployment-options"></a>Outras opções de implantação de contêiner

Além do AKS (serviço kubernetes do Azure), você também pode implantar contêineres no serviço Azure App para contêineres e instâncias de contêiner do Azure.

## <a name="when-does-it-make-sense-to-deploy-to-app-service-for-containers"></a>Quando faz sentido implantar no serviço de aplicativo para contêineres?

Aplicativos de produção simples que não exigem orquestração são adequados para Azure App serviço para contêineres.

## <a name="how-to-deploy-to-app-service-for-containers"></a>Como implantar no serviço de aplicativo para contêineres

Para implantar o [serviço de Azure app para contêineres](https://azure.microsoft.com/services/app-service/containers/), você precisará de uma instância do ACR (registro de contêiner do Azure) e de credenciais para acessá-lo. Envie por push sua imagem de contêiner para o repositório ACR para que ele possa ser inserido em seu serviço de Azure App. Uma vez concluído, você pode configurar o aplicativo para implantação contínua. Isso implantará automaticamente as atualizações sempre que a imagem for alterada no ACR.

## <a name="when-does-it-make-sense-to-deploy-to-azure-container-instances"></a>Quando faz sentido implantar em instâncias de contêiner do Azure?

As [ACI (instâncias de contêiner do Azure)](https://azure.microsoft.com/services/container-instances/) permitem que você execute contêineres do Docker em um ambiente de nuvem gerenciado e sem servidor, independentemente de ter que configurar máquinas virtuais ou clusters. É uma ótima solução para cargas de trabalho de curta execução que podem ser executadas em um contêiner isolado. Considere o ACI para serviços simples, cenários de teste, automação de tarefas e trabalhos de compilação. O ACI gira uma instância de contêiner, executa a tarefa e a gira.

## <a name="how-to-deploy-an-app-to-azure-container-instances"></a>Como implantar um aplicativo em instâncias de contêiner do Azure

Para implantar as [ACI (instâncias de contêiner do Azure)](/azure/container-instances/), você precisa de um ACR (registro de contêiner do Azure) e credenciais para acessá-lo. Depois de enviar por push sua imagem de contêiner para o repositório, ela estará disponível para efetuar pull no ACI. Você pode trabalhar com ACI usando o portal do Azure ou a interface de linha de comando. O ACR fornece integração total com o ACI. A Figura 3-14 mostra como enviar por push uma imagem de contêiner individual para o ACR.

![Instância de execução do registro de contêiner do Azure](./media/acr-runinstance-contextmenu.png)

**Figura 3-14**. Instância de execução do registro de contêiner do Azure

A criação de uma instância no ACI pode ser feita rapidamente. Especifique o registro de imagem, as informações do grupo de recursos do Azure, a quantidade de memória a ser alocada e a porta na qual escutar. Este guia [de início rápido mostra como implantar uma instância de contêiner no ACI usando o portal do Azure](/azure/container-instances/container-instances-quickstart-portal).

Quando a implantação for concluída, localize o endereço IP do contêiner implantado recentemente e comunique-se com ele pela porta especificada.

As instâncias de contêiner do Azure oferecem a maneira mais rápida de executar cargas de trabalho de contêiner simples no Azure. Você não precisa configurar um serviço de aplicativo, orquestrador ou máquina virtual. Para cenários em que você precisa de orquestração de contêiner completa, descoberta de serviço, dimensionamento automático ou atualizações coordenadas, recomendamos o serviço kubernetes do Azure (AKS).

## <a name="references"></a>Referências

- [O que é o Kubernetes?](https://blog.newrelic.com/engineering/what-is-kubernetes/)
- [Instalando o kubernetes com Minikube](https://kubernetes.io/docs/setup/learning-environment/minikube/)
- [Área de trabalho do MiniKube vs Docker](https://medium.com/containers-101/local-kubernetes-for-windows-minikube-vs-docker-desktop-25a1c6d3b766)
- [Ferramentas do Visual Studio para Docker](/dotnet/standard/containerized-lifecycle-architecture/design-develop-containerized-apps/visual-studio-tools-for-docker)
- [Entendendo a inicialização a frio sem servidor](https://azure.microsoft.com/blog/understanding-serverless-cold-start/)
- [Instâncias de Azure Functions previamente passivas](/azure/azure-functions/functions-premium-plan#pre-warmed-instances)
- [Criar uma função no Linux usando uma imagem personalizada](/azure/azure-functions/functions-create-function-linux-custom-image)
- [Executar Azure Functions em um contêiner do Docker](https://markheath.net/post/azure-functions-docker)
- [Criar uma função no Linux usando uma imagem personalizada](/azure/azure-functions/functions-create-function-linux-custom-image)
- [Azure Functions com dimensionamento automático controlado por evento kubernetes](/azure/azure-functions/functions-kubernetes-keda)
- [Versão canário](https://martinfowler.com/bliki/CanaryRelease.html)
- [Azure Dev Spaces com VS Code](/azure/dev-spaces/quickstart-netcore)
- [Azure Dev Spaces com o Visual Studio](/azure/dev-spaces/quickstart-netcore-visualstudio)
- [AKS vários pools de nós](/azure/aks/use-multiple-node-pools)
- [Autoescalar do cluster AKS](/azure/aks/cluster-autoscaler)
- [Tutorial: dimensionar aplicativos em AKS](/azure/aks/tutorial-kubernetes-scale)
- [Escala e hospedagem do Azure Functions](/azure/azure-functions/functions-scale)
- [Documentos de instâncias de contêiner do Azure](/azure/container-instances/)
- [Implantar instância de contêiner do ACR](/azure/container-instances/container-instances-using-azure-container-registry#deploy-with-azure-portal)

>[!div class="step-by-step"]
>[Anterior](scale-containers-serverless.md) 
> [Avançar](communication-patterns.md)
