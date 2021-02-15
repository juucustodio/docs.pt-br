---
title: Comunicação resiliente
description: Arquitetando aplicativos .NET nativos da nuvem para o Azure | Comunicação resiliente
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: 52f08c066767175c699f5a058267cb42d2b1d4aa
ms.sourcegitcommit: 4df8e005c074ceb1f978f007b222fe253be2baf3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99547688"
---
# <a name="resilient-communications"></a>Comunicações resilientes

Em todo este livro, adotamos uma abordagem arquitetônica baseada em microserviço. Embora essa arquitetura forneça benefícios importantes, ela apresenta muitos desafios:

- *Comunicação de rede fora do processo.* Cada microserviço se comunica em um protocolo de rede que apresenta congestionamento de rede, latência e falhas transitórias.

- *Descoberta de serviço.* Como os microserviços detectam e se comunicam uns com os outros ao serem executados em um cluster de computadores com seus próprios endereços IP e portas?

- *Resiliência.* Como gerenciar falhas de curta duração e manter o sistema estável?

- *Balanceamento de carga.* Como o tráfego de entrada é distribuído entre várias instâncias de um microserviço?

- *Segurança.* Como as questões de segurança, como criptografia de nível de transporte e gerenciamento de certificados, são impostas?

- *Monitoramento distribuído.* -Como correlacionar e capturar a rastreabilidade e o monitoramento de uma única solicitação entre vários microservices de consumo?

Você pode resolver essas preocupações com diferentes bibliotecas e estruturas, mas a implementação pode ser cara, complexa e demorada. Você também acaba com preocupações com a infraestrutura associada à lógica de negócios.

## <a name="service-mesh"></a>Malha de serviço

Uma abordagem melhor é uma tecnologia em evolução chamada *malha de serviço*. Uma [malha de serviço](https://www.nginx.com/blog/what-is-a-service-mesh/) é uma camada de infraestrutura configurável com recursos internos para lidar com a comunicação do serviço e os outros desafios mencionados acima. Ele dissocia essas preocupações movendo-as para um proxy de serviço. O proxy é implantado em um processo separado (chamado de [sidecar](/azure/architecture/patterns/sidecar)) para fornecer isolamento do código comercial. No entanto, o sidecar está vinculado ao serviço – ele é criado com ele e compartilha seu ciclo de vida. A Figura 6-7 mostra esse cenário.

![Malha de serviço com um carro lateral](./media/service-mesh-with-side-car.png)

**Figura 6-7**. Malha de serviço com um carro lateral

Na figura anterior, observe como o proxy intercepta e gerencia a comunicação entre os microserviços e o cluster.

Uma malha de serviço é dividida logicamente em dois componentes diferentes: um [plano de dados](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc) e um [plano de controle](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc). A Figura 6-8 mostra esses componentes e suas responsabilidades.

![Controle de malha de serviço e plano de dados](./media/istio-control-and-data-plane.png)

**Figura 6-8.** Controle de malha de serviço e plano de dados

Uma vez configurado, uma malha de serviço é altamente funcional. Ele pode recuperar um pool correspondente de instâncias de um ponto de extremidade de descoberta de serviço. Em seguida, a malha pode enviar uma solicitação para uma instância específica, registrando a latência e o tipo de resposta do resultado. Uma malha pode escolher a instância mais provável de retornar uma resposta rápida com base em vários fatores, incluindo sua latência observada para solicitações recentes.

Se uma instância não estiver respondendo ou falhar, a malha tentará novamente a solicitação em outra instância. Se ele retornar erros, uma malha removerá a instância do pool de balanceamento de carga e a redefinirá após o reparo. Se uma solicitação atingir o tempo limite, uma malha poderá falhar e, em seguida, repetir a solicitação. Uma malha captura e emite métricas e rastreamento distribuído para um sistema de métricas centralizado.

## <a name="istio-and-envoy"></a>İSTİO e Envoy

Embora algumas opções de malha de serviço existam atualmente, a [İSTİO](https://istio.io/docs/concepts/what-is-istio/) é a mais popular no momento da elaboração deste artigo. İSTİO é uma joint venture da IBM, do Google e do lyft. É uma oferta de código-fonte aberto que pode ser integrada a um aplicativo distribuído novo ou existente. A tecnologia fornece uma solução consistente e completa para proteger, conectar e monitorar os microserviços. Seus recursos incluem:

- Proteja a comunicação entre serviços em um cluster com autenticação e autorização baseadas em identidade forte.
- Balanceamento de carga automático para tráfego HTTP, [gRPC](https://grpc.io/), WebSocket e TCP.
- Controle refinado do comportamento de tráfego com regras de roteamento avançadas, repetições, failovers e injeção de falha.
- Uma camada de política conectável e uma API de configuração que dão suporte a controles de acesso, limites de taxa e cotas.
- Métricas, logs e rastreamentos automáticos para todo o tráfego em um cluster, incluindo a entrada e saída do cluster.

Um componente fundamental para uma implementação de İSTİO é um serviço de proxy intitulado The [Envoy proxy](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy). Ele é executado junto com cada serviço e fornece uma base independente de plataforma para os seguintes recursos:

- Descoberta dinâmica de serviço.
- Balanceamento de carga.
- Término do TLS.
- Proxies HTTP e gRPC.
- Resiliência do disjuntor.
- Verificações de integridade.
- Atualizações sem interrupção com implantações do [canário](https://martinfowler.com/bliki/CanaryRelease.html) .

Conforme discutido anteriormente, o Envoy é implantado como um sidecar para cada microserviço no cluster.

## <a name="integration-with-azure-kubernetes-services"></a>Integração com os serviços Kubernetess do Azure

A nuvem do Azure adota o İSTİO e fornece suporte direto para ele nos serviços Kubernetess do Azure. Os links a seguir podem ajudá-lo a começar:

- [Instalando o İSTİO no AKS](/azure/aks/istio-install)
- [Usando AKS e İSTİO](/azure/aks/istio-scenario-routing)

### <a name="references"></a>Referências

- [Polly](https://dotnetfoundation.org/projects/polly)

- [Padrão de repetição](/azure/architecture/patterns/retry)

- [Padrão de interruptor de circuito](/azure/architecture/patterns/circuit-breaker)

- [White paper sobre resiliência no Azure](https://azure.microsoft.com/mediahandler/files/resourcefiles/resilience-in-azure-whitepaper/Resilience%20in%20Azure.pdf)

- [latência de rede](https://www.techopedia.com/definition/8553/network-latency)

- [Redundância](/azure/architecture/guide/design-principles/redundancy)

- [replicação geográfica](/azure/sql-database/sql-database-active-geo-replication)

- [Gerenciador de Tráfego do Azure](/azure/traffic-manager/traffic-manager-overview)

- [Diretrizes de dimensionamento automático](/azure/architecture/best-practices/auto-scaling)

- [Istio](https://istio.io/docs/concepts/what-is-istio/)

- [Proxy Envoy](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy)

>[!div class="step-by-step"]
>[Anterior](infrastructure-resiliency-azure.md) 
> [Avançar](monitoring-health.md)
