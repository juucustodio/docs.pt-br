---
title: Balanceamento de carga gRPC-gRPC para desenvolvedores do WCF
description: Escolhendo um balanceador de carga para trabalhar com os serviços gRPCs.
ms.date: 12/15/2020
ms.openlocfilehash: 55f61608dce1f159b11d7265a47938ba49e9e188
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938579"
---
# <a name="load-balancing-grpc"></a>GRPC de balanceamento de carga

Uma implantação típica de um aplicativo gRPC inclui várias instâncias idênticas do serviço, fornecendo resiliência e escalabilidade horizontal. O balanceamento de carga distribui solicitações de entrada entre essas instâncias para fornecer uso total de todos os recursos disponíveis. Para tornar esse balanceamento de carga invisível para o cliente, é comum usar um servidor de balanceador de carga proxy para lidar com solicitações de clientes e roteá-las para instâncias de back-end.

Os balanceadores de carga são classificados de acordo com a *camada* em que operam. Os balanceadores de carga de camada 4 funcionam no nível de *transporte* , por exemplo, com soquetes TCP, conexões e pacotes. Os balanceadores de carga de camada 7 funcionam no nível do *aplicativo* , manipulando especificamente solicitações HTTP/2 para aplicativos gRPC.

## <a name="l4-load-balancers"></a>Balanceadores de carga L4

Um balanceador de carga L4 aceita uma solicitação de conexão TCP de um cliente, abre outra conexão com uma das instâncias de back-end e copia dados entre as duas conexões sem processamento real. O L4 oferece excelente desempenho e baixa latência, mas com pouco controle ou inteligência. Desde que o cliente mantenha a conexão aberta, todas as solicitações serão direcionadas para a mesma instância de back-end.

 [Azure Load Balancer](https://azure.microsoft.com/services/load-balancer/) é um exemplo de um balanceador de carga L4.

## <a name="l7-load-balancers"></a>Balanceadores de carga L7

Um balanceador de carga L7 analisa as solicitações HTTP/2 de entrada e as passa para as instâncias de back-end em uma base solicitação por solicitação, independentemente de quanto tempo a conexão é mantida pelo cliente.

Exemplos de balanceadores de carga L7:

- [NGINX](https://www.nginx.com/)
- [HAProxy](https://www.haproxy.com/)
- [Traefik](https://traefik.io/)

Como regra prática, os balanceadores de carga L7 são a melhor opção para gRPC e outros aplicativos HTTP/2 (e para aplicativos HTTP geralmente, de fato). Os balanceadores de carga L4 *funcionarão* com aplicativos gRPC, mas eles serão úteis principalmente quando baixa latência e baixa sobrecarga forem importantes.

> [!IMPORTANT]
> No momento da redação deste artigo, alguns balanceadores de carga L7 não dão suporte a todas as partes da especificação HTTP/2 exigidas pelos serviços gRPCs, como cabeçalhos à direita.

Se você estiver usando a criptografia TLS, os balanceadores de carga podem encerrar a conexão TLS e passar solicitações não criptografadas para o aplicativo de back-end, ou podem passar a solicitação criptografada ao longo do. De qualquer forma, o balanceador de carga precisará ser configurado com a chave pública e privada do servidor para que ele possa descriptografar solicitações de processamento.

Consulte a documentação do balanceador de carga preferencial para descobrir como configurá-lo para lidar com solicitações HTTP/2 com seus serviços de back-end.

## <a name="load-balancing-within-kubernetes"></a>Balanceamento de carga dentro de kubernetes

Consulte [a seção sobre malhas de serviço](service-mesh.md) para obter uma discussão sobre o balanceamento de carga entre serviços internos no kubernetes.

>[!div class="step-by-step"]
>[Anterior](service-mesh.md) 
> [Avançar](application-performance-management.md)
