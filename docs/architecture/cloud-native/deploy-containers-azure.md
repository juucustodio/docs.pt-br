---
title: Como implantar contêineres no Azure
description: Implantando contêineres no Azure com o registro de contêiner do Azure, o serviço kubernetes do Azure e o Azure Dev Spaces.
ms.date: 04/13/2020
ms.openlocfilehash: d848a146a2bdb5d8d02543f57f19d6a39c9699e6
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91160769"
---
# <a name="deploying-containers-in-azure"></a>Como implantar contêineres no Azure

Discutimos os contêineres neste capítulo e no capítulo 1. Vimos que os contêineres fornecem muitos benefícios para aplicativos nativos de nuvem, incluindo portabilidade. Na nuvem do Azure, você pode implantar os mesmos serviços em contêineres em ambientes de preparo e produção. O Azure fornece várias opções para hospedar essas cargas de trabalho em contêineres:

- AKS (Serviços do Kubernetes do Azure)
- ACI (Instância de Contêiner do Azure)
- Aplicativos Web para contêineres do Azure

## <a name="azure-container-registry"></a>Registro de Contêiner do Azure

Ao colocar um microserviço em contêiner, você primeiro cria um contêiner de compilação "imagem". A imagem é uma representação binária do código de serviço, das dependências e do tempo de execução. Embora seja possível criar manualmente uma imagem usando o `Docker Build` comando da API do Docker, uma abordagem melhor é criá-la como parte de um processo de compilação automatizado.

Depois de criadas, as imagens de contêiner são armazenadas em registros de contêiner. Eles permitem que você crie, armazene e gerencie imagens de contêiner. Há vários registros disponíveis, públicos e privados. O ACR (registro de contêiner do Azure) é um serviço de registro de contêiner totalmente gerenciado na nuvem do Azure. Ele persiste suas imagens dentro da rede do Azure, reduzindo o tempo para implantá-las nos hosts de contêiner do Azure. Você também pode protegê-los usando os mesmos procedimentos de segurança e identidade que você usa para outros recursos do Azure.

Você cria um registro de contêiner do Azure usando as ferramentas [portal do Azure](/azure/container-registry/container-registry-get-started-portal), [CLI do Azure](/azure/container-registry/container-registry-get-started-azure-cli)ou [PowerShell](/azure/container-registry/container-registry-get-started-powershell). A criação de um registro no Azure é simples. Ele requer uma assinatura do Azure, um grupo de recursos e um nome exclusivo. A Figura 3-11 mostra as opções básicas para a criação de um registro, que será hospedado em `registryname.azurecr.io` .

![Criar um registro de contêiner](./media/create-container-registry.png)

**Figura 3-11**. Criar um registro de contêiner

Depois de criar o registro, você precisará autenticar com ele antes de poder usá-lo. Normalmente, você fará logon no registro usando o comando CLI do Azure:

```azurecli
az acr login --name *registryname*
```

Depois de autenticado, você pode usar comandos do Docker para enviar imagens de contêiner para ele. Para poder fazer isso, no entanto, você deve marcar sua imagem com o nome totalmente qualificado (URL) do seu servidor de logon do ACR. Ele terá o formato *registryname*. azurecr.IO.

```console
docker tag mycontainer myregistry.azurecr.io/mycontainer:v1
```

Depois de ter marcado a imagem, use o `docker push` comando para enviar a imagem por push para a instância do ACR.

```console
docker push myregistry.azurecr.io/mycontainer:v1
```

Depois de enviar uma imagem por push para o registro, é uma boa ideia remover a imagem do ambiente do Docker local, usando este comando:

```console
docker rmi myregistry.azurecr.io/mycontainer:v1
```

Como prática recomendada, os desenvolvedores não devem enviar por push as imagens manualmente para um registro de contêiner. Em vez disso, um pipeline de compilação definido em uma ferramenta como GitHub ou Azure DevOps deve ser responsável por esse processo. Saiba mais no [capítulo DevOps de nuvem nativa](devops.md).

## <a name="acr-tasks"></a>Tarefas do ACR

[As tarefas ACR](/azure/container-registry/container-registry-tasks-overview) são um conjunto de recursos disponíveis no registro de contêiner do Azure. Ele estende seu [ciclo de desenvolvimento de loop interno](../containerized-lifecycle/design-develop-containerized-apps/docker-apps-inner-loop-workflow.md) criando e gerenciando imagens de contêiner na nuvem do Azure. Em vez de invocar um `docker build` e `docker push` localmente em seu computador de desenvolvimento, eles são automaticamente tratados por tarefas de ACR na nuvem.

O comando AZ CLI a seguir cria uma imagem de contêiner e a envia para o ACR:

```azurecli
# create a container registry
az acr create --resource-group myResourceGroup --name myContainerRegistry008 --sku Basic

# build container image in ACR and push it into your container regsitry
az acr build --image sample/hello-world:v1  --registry myContainerRegistry008 --file Dockerfile .
```

Como você pode ver no bloco de comando anterior, não há necessidade de instalar o Docker desktop em seu computador de desenvolvimento. Além disso, você pode configurar gatilhos de tarefa ACR para recriar imagens de contêineres no código-fonte e nas atualizações da imagem de base.

## <a name="azure-kubernetes-service"></a>Serviço de Kubernetes do Azure

Discutimos o AKS (serviço kubernetes do Azure) no comprimento deste capítulo. Vimos que é o orquestrador de contêineres de fato gerenciar aplicativos nativos de nuvem em contêineres.

Depois de implantar uma imagem em um registro, como o ACR, você pode configurar o AKS para efetuar pull e implantá-lo automaticamente. Com um pipeline de CI/CD em vigor, você pode configurar uma estratégia de  [liberação canário](https://martinfowler.com/bliki/CanaryRelease.html) para minimizar o risco envolvido ao implantar atualizações rapidamente. A nova versão do aplicativo é inicialmente configurada em produção, sem nenhum tráfego roteado para ele. Em seguida, o sistema roteará uma pequena porcentagem de usuários para a versão implantada recentemente. À medida que a equipe ganha confiança na nova versão, ela pode distribuir mais instâncias e desativar o antigo. O AKS dá suporte facilmente a esse estilo de implantação.

Assim como acontece com a maioria dos recursos no Azure, você pode criar um cluster do serviço kubernetes do Azure usando o portal, a linha de comando ou as ferramentas de automação, como Helm ou Terraform. Para começar a usar um novo cluster, você precisa fornecer as seguintes informações:

- Assinatura do Azure
- Grupo de recursos
- Nome do cluster kubernetes
- Região
- Versão do Kubernetes
- Prefixo do nome DNS
- Tamanho do nó
- Contagem de nós

Essas informações são suficientes para começar. Como parte do processo de criação no portal do Azure, você também pode configurar opções para os seguintes recursos do cluster:

- Escala
- Autenticação
- Rede
- Monitoramento
- Marcações

Este [Guia de início rápido orienta a implantação de um cluster AKs usando o portal do Azure](/azure/aks/kubernetes-walkthrough-portal).

## <a name="azure-dev-spaces"></a>Azure Dev Spaces

Os aplicativos nativos de nuvem podem crescer de forma rápida e complexa, exigindo recursos de computação significativos para serem executados. Nesses cenários, o aplicativo inteiro não pode ser hospedado em um computador de desenvolvimento (especialmente um laptop). Azure Dev Spaces foi projetado para resolver esse problema usando AKS. Ele permite que os desenvolvedores trabalhem com uma versão local de seus serviços enquanto hospedam o restante do aplicativo em um cluster de desenvolvimento AKS.

Os desenvolvedores compartilham uma instância em execução (desenvolvimento) em um cluster AKS que contém o aplicativo em contêineres inteiro. Mas eles usam espaços pessoais configurados em sua máquina para desenvolver localmente seus serviços. Quando estiver pronto, eles serão testados de ponta a ponta no cluster AKS, sem replicar dependências. Azure Dev Spaces mescla o código do computador local com serviços no AKS. Os desenvolvedores podem iterar e depurar rapidamente o código diretamente no kubernetes usando o Visual Studio ou o Visual Studio Code.

Para entender o valor de Azure Dev Spaces, deixe-me compartilhar essa citação de Gabe Monroy, PM Lead dos contêineres em Microsoft Azure:

> "Imagine que você seja um novo funcionário tentando corrigir um bug em um aplicativo de microserviços complexos que consiste em dezenas de componentes, cada um com sua própria configuração e serviços de apoio. Para começar, você deve configurar seu ambiente de desenvolvimento local para que ele possa imitar a produção, incluindo a configuração de seu IDE, criação de cadeia de ferramentas, dependências de serviço em contêineres, um ambiente kubernetes local, simulações para fazer backup de serviços e muito mais. Com o tempo todo envolvido na configuração de seu ambiente de desenvolvimento, corrigir esse primeiro bug pode levar dias.
> Ou você pode usar espaços de desenvolvimento e AKS. "

O processo para trabalhar com Azure Dev Spaces envolve as seguintes etapas:

1. Crie o espaço de desenvolvimento.
2. Configure o espaço de desenvolvimento raiz.
3. Configure um espaço de desenvolvimento filho (para sua própria versão do sistema).
4. Conecte-se ao espaço de desenvolvimento.

Todas essas etapas podem ser executadas usando o CLI do Azure e novas  `azds` ferramentas de linha de comando. Por exemplo, para criar um novo espaço de desenvolvimento do Azure para um determinado cluster kubernetes, você usaria um comando como este:

```azurecli
az aks use-dev-spaces -g my-aks-resource-group -n MyAKSCluster
```

Em seguida, você pode usar o `azds prep` comando para gerar os ativos necessários do Docker e do gráfico Helm para executar o aplicativo. Em seguida, você executa seu código no AKS usando `azds up` . Na primeira vez que você executar esse comando, o gráfico Helm será instalado. Os contêineres serão criados e implantados de acordo com suas instruções. Essa tarefa pode levar alguns minutos na primeira vez em que for executada. No entanto, depois de fazer alterações, você pode se conectar ao seu próprio espaço de desenvolvimento filho usando `azds space select` e, em seguida, implantar e depurar suas atualizações em seu espaço de desenvolvimento filho isolado. Depois que o seu espaço de desenvolvimento estiver em funcionamento, você poderá enviar atualizações para ele emitindo o `azds up` comando novamente ou pode usar as ferramentas internas no Visual Studio ou Visual Studio Code. Com VS Code, você usa a paleta de comandos para se conectar ao seu espaço de desenvolvimento. A Figura 3-12 mostra como iniciar seu aplicativo Web usando o Azure Dev Spaces no Visual Studio.

![Conecte-se a Azure Dev Spaces no Visual Studio ](./media/azure-dev-spaces-visual-studio-launchsettings.png)
 **Figura 3-12**. Conectar-se a Azure Dev Spaces no Visual Studio

>[!div class="step-by-step"]
>[Anterior](combine-containers-serverless-approaches.md) 
> [Avançar](scale-containers-serverless.md)
