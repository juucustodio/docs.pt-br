---
title: Resiliência nativa de nuvem
description: Arquitetando aplicativos .NET nativos da nuvem para o Azure | Resiliência nativa na nuvem
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: 5c4fb261515c151fd666cc33cbb020447716c814
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91163551"
---
# <a name="cloud-native-resiliency"></a>Resiliência nativa de nuvem

A resiliência é a capacidade do seu sistema de reagir à falha e ainda continuar funcionando. Não está prestes a evitar falhas, mas aceitando falhas e construindo seus serviços nativos de nuvem para responder a ela. Você deseja retornar a um estado totalmente funcional o mais rápido possível.

Ao contrário dos aplicativos monolíticos tradicionais, onde tudo é executado juntos em um único processo, os sistemas nativos de nuvem adotam uma arquitetura distribuída, como mostrado na Figura 6-1:

![Ambiente nativo de nuvem distribuída](./media/distributed-cloud-native-environment.png)

**Figura 6-1.** Ambiente nativo de nuvem distribuída

Na figura anterior, cada microserviço e [serviço de backup](https://12factor.net/backing-services) baseado em nuvem é executado em um processo separado, na infraestrutura de servidor, comunicando-se por meio de chamadas baseadas em rede.

Operando nesse ambiente, um serviço deve ser sensível a muitos desafios diferentes:

- Latência de rede inesperada-o tempo para uma solicitação de serviço viajar para o receptor e vice-versa.

- [Falhas transitórias](/azure/architecture/best-practices/transient-faults) -erros de conectividade de rede de curta duração.

- Bloqueio por uma operação síncrona de execução longa.

- Um processo de host que falhou e está sendo reiniciado ou movido.

- Um microserviço sobrecarregado que não pode responder por um curto período de tempo.

- Uma operação de orquestrador em andamento, como uma atualização sem interrupção ou movendo um serviço de um nó para outro.

- Falhas de hardware.

As plataformas de nuvem podem detectar e atenuar muitos desses problemas de infraestrutura. Ele pode reiniciar, escalar horizontalmente e até mesmo redistribuir seu serviço para um nó diferente.  No entanto, para aproveitar ao máximo essa proteção interna, você deve projetar seus serviços para reagir a ele e prosperar nesse ambiente dinâmico.

Nas seções a seguir, exploraremos técnicas defensivas que o serviço e os recursos de nuvem gerenciados podem aproveitar para minimizar o tempo de inatividade e a interrupção.

>[!div class="step-by-step"]
>[Anterior](elastic-search-in-azure.md) 
> [Avançar](application-resiliency-patterns.md)
