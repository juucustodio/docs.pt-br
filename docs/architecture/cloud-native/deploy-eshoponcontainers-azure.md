---
title: Como implantar o eShopOnContainers no Azure
description: Implantando o aplicativo eShopOnContainers usando o serviço kubernetes do Azure, o Helm e o DevSpaces.
ms.date: 01/19/2021
ms.openlocfilehash: 8fc1343eac7f03c984c3a279d5a8c7908e37f0d1
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505785"
---
# <a name="deploying-eshoponcontainers-to-azure"></a>Como implantar o eShopOnContainers no Azure

O aplicativo eShopOnContainers pode ser implantado em várias plataformas do Azure. A abordagem recomendada é implantar o aplicativo nos AKS (serviços Kubernetess do Azure). O Helm, uma ferramenta de implantação do kubernetes, está disponível para reduzir a complexidade da implantação. Opcionalmente, os desenvolvedores podem implementar Azure Dev Spaces para kubernetes para simplificar seu processo de desenvolvimento.

## <a name="azure-kubernetes-service"></a>Serviço de Kubernetes do Azure

Para hospedar eShop em AKS, a primeira etapa é criar um cluster AKS. Para fazer isso, você pode usar o portal do Azure, que irá orientá-lo pelas etapas necessárias. Você também pode criar um cluster do CLI do Azure, tomando cuidado para habilitar o controle de acesso Role-Based (RBAC) e o roteamento de aplicativos. A documentação do eShopOnContainers ' fornece detalhes sobre as etapas para criar seu próprio cluster AKS. Depois de criado, você pode acessar e gerenciar o cluster no painel do kubernetes.

Agora você pode implantar o aplicativo eShop no cluster usando o Helm.

## <a name="deploying-to-azure-kubernetes-service-using-helm"></a>Implantando no serviço kubernetes do Azure usando o Helm

Helm é uma ferramenta de Gerenciador de pacotes de aplicativos que funciona diretamente com o kubernetes. Ele ajuda a definir, instalar e atualizar aplicativos kubernetes. Embora aplicativos simples possam ser implantados em AKS com scripts CLI personalizados ou arquivos de implantação simples, aplicativos complexos podem conter muitos objetos kubernetes e se beneficiarem do Helm.

Usando o Helm, os aplicativos incluem arquivos de configuração baseados em texto, chamados de gráficos Helm, que descrevem declarativamente o aplicativo e a configuração em pacotes Helm. Os gráficos usam arquivos padrão formatados por YAML para descrever um conjunto relacionado de recursos do kubernetes. Eles têm controle de versão junto com o código do aplicativo que eles descrevem. Os gráficos Helm variam de simples a complexo, dependendo dos requisitos da instalação que descrevem.

O Helm é composto por uma ferramenta de cliente de linha de comando, que consome gráficos do Helm e inicia comandos para um componente de servidor chamado, o. O gaveta se comunica com a API do kubernetes para garantir o provisionamento correto de suas cargas de trabalho em contêineres. O Helm é mantido pela base de computação nativa de nuvem.

O seguinte arquivo YAML apresenta um modelo Helm:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ .Values.app.svc.marketing }}
  labels:
    app: {{ template "marketing-api.name" . }}
    chart: {{ template "marketing-api.chart" . }}
    release: {{ .Release.Name }}
    heritage: {{ .Release.Service }}
spec:
  type: {{ .Values.service.type }}
  ports:
    - port: {{ .Values.service.port }}
      targetPort: http
      protocol: TCP
      name: http
  selector:
    app: {{ template "marketing-api.name" . }}
    release: {{ .Release.Name }}
```

Observe como o modelo descreve um conjunto dinâmico de pares chave/valor. Quando o modelo é invocado, os valores que estão entre chaves são extraídos de outros arquivos de configuração baseados em YAML.

Você encontrará os gráficos eShopOnContainers Helm na pasta/K8S/Helm. A Figura 2-6 mostra como os diferentes componentes do aplicativo são organizados em uma estrutura de pastas usada pelo Helm para definir e implantações gerenciadas.

![Arquitetura eShopOnContainers ](./media/eshoponcontainers-helm-folder.png)
 **Figura 2-6**. A pasta eShopOnContainers Helm

Cada componente individual é instalado usando um `helm install` comando. o eShop inclui um script "implantar tudo" que percorre e instala os componentes usando seus respectivos gráficos do Helm. O resultado é um processo repetível, com versão com o aplicativo no controle do código-fonte, que qualquer pessoa da equipe pode implantar em um cluster AKS com um comando de script de uma linha.

> Observe que a versão 3 do Helm remove oficialmente a necessidade do componente de servidor da gaveta. Mais informações sobre esse aprimoramento podem ser encontradas [aqui](https://medium.com/better-programming/why-is-tiller-missing-in-helm-3-2347c446714).

## <a name="azure-dev-spaces"></a>Azure Dev Spaces

Os aplicativos nativos de nuvem podem crescer de forma rápida e complexa, exigindo recursos de computação significativos para serem executados. Nesses cenários, o aplicativo inteiro não pode ser hospedado em um computador de desenvolvimento (especialmente um laptop). Azure Dev Spaces foi projetado para resolver esse problema usando AKS. Ele permite que os desenvolvedores trabalhem com uma versão local de seus serviços enquanto hospedam o restante do aplicativo em um cluster de desenvolvimento AKS.

Os desenvolvedores compartilham uma instância em execução (desenvolvimento) em um cluster AKS que contém o aplicativo em contêineres inteiro. Mas eles usam espaços pessoais configurados em sua máquina para desenvolver localmente seus serviços. Quando estiver pronto, eles serão testados de ponta a ponta no cluster AKS, sem replicar dependências. Azure Dev Spaces mescla o código do computador local com serviços no AKS. Os membros da equipe podem ver como suas alterações se comportarão em um ambiente AKS real. Os desenvolvedores podem iterar e depurar rapidamente o código diretamente no kubernetes usando o Visual Studio 2017 ou Visual Studio Code.

Na Figura 2-7, você pode ver que o desenvolvedor Susana implantou uma versão atualizada do microserviço bikes em seu espaço de desenvolvimento. Em seguida, ela é capaz de testar suas alterações usando uma URL personalizada que começa com o nome de seu espaço (susie.s.dev.myapp.eus.azds.io).

![Arquitetura eShopOnContainers ](./media/azure-devspaces-one.png)
 **Figura 2-7**. O Developer Susana implanta sua própria versão do microserviço Bikes e a testa.

Ao mesmo tempo, o desenvolvedor John está Personalizando o microserviço de reservas e precisa testar suas alterações. Ele implanta suas alterações em seu próprio espaço de desenvolvimento sem entrar em conflito com as alterações do Susana, conforme mostrado na Figura 2-8. João, em seguida, testa suas alterações usando sua própria URL que é prefixada com o nome de seu espaço (john.s.dev.myapp.eus.azds.io).

![Arquitetura eShopOnContainers ](./media/azure-devspaces-two.png)
 **Figura 2-8**. O desenvolvedor John implanta sua própria versão do microserviço de reservas e a testa sem entrar em conflito com outros desenvolvedores.

Usando Azure Dev Spaces, as equipes podem trabalhar diretamente com o AKS enquanto alteram, implantam e testam suas alterações de forma independente. Essa abordagem reduz a necessidade de ambientes hospedados dedicados separados, pois cada desenvolvedor efetivamente tem seu próprio ambiente AKS. Os desenvolvedores podem trabalhar com Azure Dev Spaces usando sua CLI ou iniciar seu aplicativo para Azure Dev Spaces diretamente do Visual Studio. [Saiba mais sobre como Azure Dev Spaces funciona e está configurado.](/azure/dev-spaces/how-dev-spaces-works)

## <a name="azure-functions-and-logic-apps-serverless"></a>Azure Functions e aplicativos lógicos (sem servidor)

O exemplo de eShopOnContainers inclui suporte para acompanhamento de campanhas de marketing online. Uma função do Azure é usada para acompanhar os detalhes da campanha de marketing para uma determinada ID de campanha. Em vez de criar um Microservice completo, uma única função do Azure é mais simples e suficiente. Azure Functions ter um modelo simples de compilação e implantação, especialmente quando configurado para ser executado no kubernetes. A implantação da função é inserida em script usando modelos de Azure Resource Manager (ARM) e a CLI do Azure. Este serviço de campanha não é voltado para o cliente e invoca uma única operação, tornando-o um excelente candidato para Azure Functions. A função requer configuração mínima, incluindo uma cadeia de conexão de banco de dados e configurações de URI de base de imagem. Você configura Azure Functions no portal do Azure.

>[!div class="step-by-step"]
>[Anterior](map-eshoponcontainers-azure-services.md) 
> [Avançar](centralized-configuration.md)
