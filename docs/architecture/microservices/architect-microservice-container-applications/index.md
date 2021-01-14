---
title: Como arquitetar aplicativos baseados em contêineres e em microsserviços
description: Arquitetar aplicativos baseados em contêineres e em microsserviços não é simples e deve ser levado a sério. Aprenda os conceitos principais neste capítulo.
ms.date: 01/13/2021
ms.openlocfilehash: d87633b6c5073a9098c34c1192bcca1abad00e5c
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189480"
---
# <a name="architecting-container-and-microservice-based-applications"></a>Como arquitetar aplicativos baseados em contêineres e em microsserviços

*Os microserviços oferecem ótimos benefícios, mas também geram novos desafios enormes. Os padrões de arquitetura de microserviço são pilares fundamentais ao criar um aplicativo baseado em microserviço.*

Antes neste guia, você aprendeu os conceitos básicos sobre contêineres e sobre o Docker. Essa informação era o mínimo necessário para começar a usar contêineres. Mesmo que os contêineres sejam habilitadores e uma ótima opção para os microserviços, eles não são obrigatórios para uma arquitetura de microserviço e muitos conceitos arquitetônicos nessa seção de arquitetura também poderiam ser aplicados sem contêineres. No entanto, este guia concentra-se na interseção de ambos devido a importância dos contêineres que já foi apresentada.

Os aplicativos corporativos podem ser complexos e geralmente são compostos de vários serviços e não em um único serviço. Para esses casos, você precisa entender outras abordagens de arquitetura, como os microserviço e determinados padrões de design de Domain-Driven (DDD), além dos conceitos de orquestração de contêineres. Observe que este capítulo não descreve apenas microsserviços em contêineres, mas também qualquer aplicativo em contêiner.

## <a name="container-design-principles"></a>Princípios de design de contêiner

No modelo de contêiner, uma instância de imagem de contêiner representa um único processo. Definindo uma imagem de contêiner como um limite de processo, você pode criar primitivas que podem ser usadas para dimensionar o processo ou criar um lote.

Ao criar uma imagem de contêiner, você verá uma definição [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) no Dockerfile. Essa definição define o processo cujo tempo de vida controla o tempo de vida do contêiner. Quando o processo for concluído, o ciclo de vida do contêiner será encerrado. Os contêineres podem representar processos de longa execução como servidores Web, mas também podem representar processos de curta duração, como trabalhos em lotes, que anteriormente talvez eram implementados como Azure [WebJobs](https://github.com/Azure/azure-webjobs-sdk/wiki).

Se o processo falhar, o contêiner é encerrado e o orquestrador assume. Se o orquestrador foi configurado para manter cinco instâncias em execução e uma falhar, ele criará outra instância de contêiner para substituir o processo com falha. Em um trabalho em lotes, o processo é iniciado com parâmetros. Quando o processo é concluído, o trabalho é concluído. Mais tarde, este guia faz drill-down em orquestradores.

Você pode encontrar um cenário em que deseje vários processos em execução em um único contêiner. Para esse cenário, como pode haver apenas um ponto de entrada por contêiner, você poderá executar um script dentro do contêiner para iniciar quantos programas forem necessários. Por exemplo, você pode usar o [Supervisor](http://supervisord.org/) ou uma ferramenta semelhante para cuidar da inicialização de vários processos dentro de um único contêiner. No entanto, mesmo que seja possível encontrar arquiteturas com vários processos por contêiner, essa abordagem não é muito comum.

>[!div class="step-by-step"]
>[Anterior](../net-core-net-framework-containers/official-net-docker-images.md) 
> [Avançar](containerize-monolithic-applications.md)
