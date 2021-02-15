---
title: Capacidade de endereçamento de microsserviços e o Registro do serviço
description: Entenda a função dos Registros de imagem de contêiner na arquitetura de microsserviços.
ms.date: 01/13/2021
ms.openlocfilehash: 363a307d44d30125563863bbe3ebeb5f5b9ad2bc
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188407"
---
# <a name="microservices-addressability-and-the-service-registry"></a>Capacidade de endereçamento de microsserviços e o Registro do serviço

Cada microsserviço tem um nome exclusivo (URL) usado para resolver sua localização. O microsserviço precisa ser endereçável independentemente do local em que está sendo executado. Se você tiver que pensar em qual computador está executando um microsserviço específico, as coisas poderão se complicar rapidamente. Da mesma forma que o DNS resolve uma URL para um determinado computador, seu microsserviço precisa ter um nome exclusivo para que seu local atual seja detectável. Os microsserviços precisam de nomes endereçáveis que os tornem independentes da infraestrutura na qual eles estão sendo executados. Essa abordagem implica que há uma interação entre como o serviço é implantado e como ele é descoberto, pois precisa haver um [registro de serviço](https://microservices.io/patterns/service-registry.html). Do mesmo modo, quando um computador falha, o serviço de Registro deve ser capaz de indicar o local em que o serviço está sendo executado no momento.

O [padrão de Registro de serviço](https://microservices.io/patterns/service-registry.html) é uma parte importante da descoberta de serviço. O Registro é um banco de dados que contém os locais de rede das instâncias de serviço. Um Registro de serviço precisa ser atualizado e estar altamente disponível. Os clientes podem armazenar locais de rede em cache obtidos do Registro de serviço. No entanto, essas informações eventualmente ficam desatualizadas e os clientes não podem mais descobrir instâncias de serviço. Portanto, um registro de serviço consiste em um cluster de servidores que usam um protocolo de replicação para manter a consistência.

Em alguns ambientes de implantação de microserviço (chamados de clusters, para serem abordados em uma seção posterior), a descoberta de serviço é interna. Por exemplo, um ambiente do AKS (Serviço de Contêiner do Azure com Kubernetes) pode manipular o registro e o cancelamento de registro da instância de serviço. Ele também executa um proxy em cada host de cluster que desempenha a função de roteador de descoberta do servidor.

## <a name="additional-resources"></a>Recursos adicionais

- **Chris Richardson. Padrão: registro de serviço** \
  <https://microservices.io/patterns/service-registry.html>

- **Auth0. O registro do serviço** \
  <https://auth0.com/blog/an-introduction-to-microservices-part-3-the-service-registry/>

- **Gabriel Schenker. Descoberta de serviço** \
  <https://lostechies.com/gabrielschenker/2016/01/27/service-discovery/>

>[!div class="step-by-step"]
>[Anterior](maintain-microservice-apis.md) 
> [Avançar](microservice-based-composite-ui-shape-layout.md)
