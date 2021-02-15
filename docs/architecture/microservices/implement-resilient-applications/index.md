---
title: Implementar aplicativos resilientes
description: Saiba mais sobre a resiliência, um conceito central na arquitetura de microsserviços. Você deve saber como lidar com falhas transitórias normalmente quando elas ocorrem.
ms.date: 01/30/2020
ms.openlocfilehash: 3ed4474eaa1225e80f05db86965e4ba53b5d2301
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100429319"
---
# <a name="implement-resilient-applications"></a>Implementar aplicativos resilientes

*Seu microserviço e seus aplicativos baseados em nuvem devem adotar as falhas parciais que certamente ocorrerão eventualmente. Você deve projetar seu aplicativo para ser resiliente a essas falhas parciais.*

A resiliência é a capacidade de se recuperar de falhas e continuar funcionando. Não se trata de evitar falhas, mas de aceitar o fato de que as falhas acontecerão, e responder a elas de uma maneira que evite tempo de inatividade ou perda de dados. A meta de resiliência é retornar o aplicativo para um estado totalmente funcional após uma falha.

Já é um grande desafio criar e implantar um aplicativo baseado em microsserviços. E você ainda precisa manter o aplicativo em execução em um ambiente em que algum tipo de falha certamente ocorrerá. Portanto, seu aplicativo precisa ser resiliente. Ele deve ser projetado para lidar com falhas parciais, como interrupções da rede ou falhas de nós ou de VMs na nuvem. Até mesmo os microsserviços (contêineres) que estão sendo movidos para outro nó em um cluster podem causar falhas curtas intermitentes no aplicativo.

Os diversos componentes individuais do aplicativo também precisam incorporar recursos de monitoramento de integridade. Seguindo as diretrizes neste capítulo, você poderá criar um aplicativo que pode funcionar perfeitamente apesar do tempo de inatividade temporário ou das interrupções normais que ocorrem em implantações complexas e baseadas em nuvem.

>[!IMPORTANT]
> eShopOnContainer tinha usado a [biblioteca Polly](https://thepollyproject.azurewebsites.net/) para implementar a resiliência usando [clientes digitados](./use-httpclientfactory-to-implement-resilient-http-requests.md) até a versão 3.0.0.
>
> A partir da versão 3.0.0, a resiliência das chamadas HTTP é implementada usando uma [malha Linkerd](https://linkerd.io/), que trata as repetições de uma maneira transparente e configurável, em um cluster kubernetes, sem a necessidade de lidar com essas preocupações no código.
>
> A biblioteca Polly ainda é usada para adicionar resiliência a conexões de banco de dados, especialmente ao iniciar os serviços.

>[!WARNING]
> Todos os exemplos de código nesta seção eram válidos antes de usar Linkerd e não são atualizados para refletir o código real atual. Eles fazem sentido no contexto desta seção.

>[!div class="step-by-step"]
>[Anterior](../microservice-ddd-cqrs-patterns/microservice-application-layer-implementation-web-api.md) 
> [Avançar](handle-partial-failure.md)
