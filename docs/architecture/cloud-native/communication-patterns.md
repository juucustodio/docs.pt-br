---
title: Padrões de comunicação nativos de nuvem
description: Saiba mais sobre as principais preocupações de comunicação do serviço em aplicativos nativos de nuvem
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: 5ce789924e828865f7bdf717b081b9112203293a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91160912"
---
# <a name="cloud-native-communication-patterns"></a>Padrões de comunicação nativos de nuvem

Ao construir um sistema nativo de nuvem, a comunicação se torna uma decisão de design significativa. Como um aplicativo cliente front-end se comunica com um microserviço de back-end? Como os microserviços de back-end se comunicam entre si? Quais são os princípios, padrões e práticas recomendadas a serem considerados ao implementar a comunicação em aplicativos nativos de nuvem?

## <a name="communication-considerations"></a>Considerações de comunicação

Em um aplicativo monolítico, a comunicação é simples. Os módulos de código são executados juntos no mesmo espaço executável (processo) em um servidor. Essa abordagem pode ter vantagens de desempenho à medida que tudo é executado juntos na memória compartilhada, mas resulta em um código rigidamente acoplado que se torna difícil de manter, evoluir e dimensionar.

Os sistemas nativos de nuvem implementam uma arquitetura baseada em microserviço com muitos microserviços pequenos e independentes. Cada microserviço é executado em um processo separado e normalmente é executado dentro de um contêiner implantado em um *cluster*.

Um cluster agrupa um pool de máquinas virtuais para formar um ambiente altamente disponível. Eles são gerenciados com uma ferramenta de orquestração, que é responsável por implantar e gerenciar os microserviços em contêineres. A Figura 4-1 mostra um cluster [kubernetes](https://kubernetes.io) implantado na nuvem do Azure com os [serviços de kubernetes do Azure](/azure/aks/intro-kubernetes)totalmente gerenciados.

![Um cluster kubernetes no Azure](./media/kubernetes-cluster-in-azure.png)

**Figura 4-1**. Um cluster kubernetes no Azure

No cluster, os microserviços se comunicam entre si por meio de APIs e tecnologias de mensagens.

Embora eles forneçam muitos benefícios, os microserviços não são um almoço gratuito. As chamadas de método local no processo entre componentes agora são substituídas por chamadas de rede. Cada microserviço deve se comunicar por um protocolo de rede, o que adiciona complexidade ao seu sistema:

- O congestionamento da rede, a latência e as falhas transitórias são uma preocupação constante.

- A resiliência (ou seja, repetindo solicitações com falha) é essencial.

- Algumas chamadas devem ser [idempotentes](https://www.restapitutorial.com/lessons/idempotency.html) como para manter o estado consistente.

- Cada microserviço deve autenticar e autorizar chamadas.

- Cada mensagem deve ser serializada e, em seguida, desserializada – o que pode ser caro.

- A criptografia/descriptografia de mensagens se torna importante.

Os [microserviços do Book .net: arquitetura para aplicativos .net em contêineres](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook), disponíveis gratuitamente da Microsoft, fornece uma cobertura aprofundada dos padrões de comunicação para aplicativos de microatendimento. Neste capítulo, fornecemos uma visão geral de alto nível desses padrões, juntamente com as opções de implementação disponíveis na nuvem do Azure.

Neste capítulo, primeiro abordaremos a comunicação entre os aplicativos de front-end e os microserviços de back-end. Em seguida, veremos que os microserviços de back-end se comunicam entre si. Exploraremos a tecnologia de comunicação para cima e gRPC. Por fim, examinaremos os novos padrões de comunicação inovadores usando a tecnologia de malha de serviço. Também veremos como a nuvem do Azure fornece diferentes tipos de *serviços de backup* para dar suporte à comunicação nativa de nuvem.

>[!div class="step-by-step"]
>[Anterior](other-deployment-options.md) 
> [Avançar](front-end-communication.md)
