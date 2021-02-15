---
title: Comunicação em uma arquitetura de microsserviço
description: Explore diferentes maneiras de comunicação entre microsserviços, compreendendo as implicações de maneiras síncronas e assíncronas.
ms.date: 01/30/2020
ms.openlocfilehash: a918ea7573d7402a82d2df2c63301e4838fa66dc
ms.sourcegitcommit: 88fbb019b84c2d044d11fb4f6004aec07f2b25b1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97899594"
---
# <a name="communication-in-a-microservice-architecture"></a>Comunicação em uma arquitetura de microsserviço

Em um aplicativo monolítico em execução em um único processo, os componentes invocam-se usando um método no nível da linguagem ou chamadas de função. Eles poderão ser fortemente acoplados se você estiver criando objetos com código (por exemplo, `new ClassName()`) ou poderão ser invocados de forma desacoplada, se você estiver usando injeção de dependência referenciando abstrações em vez de instâncias concretas de objeto. De qualquer forma, os objetos são executados no mesmo processo. O maior desafio ao passar de um aplicativo monolítico para um aplicativo baseado em microsserviços é alterar o mecanismo de comunicação. Uma conversão direta das chamadas de método internas em processo em chamadas RPC para os serviços causará uma comunicação muito intensa e ineficiente que não terá um bom desempenho em ambientes distribuídos. Os desafios da criação adequada de um sistema distribuído são tão conhecidos que existe um código conhecido como [Fallacies of distributed computing](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing) (Enganos da computação distribuída) que lista as suposições que os desenvolvedores geralmente fazem ao passar de designs monolíticos para designs distribuídos.

Não há apenas uma solução, mas várias. Uma das soluções envolve isolar os microsserviços de negócios o máximo possível. Em seguida, usar a comunicação assíncrona entre os microsserviços internos e substituir a comunicação refinada típica na comunicação entre processos dos objetos por uma comunicação menos refinada. Você pode fazer isso agrupando chamadas e retornando para o cliente dados que agregam os resultados de várias chamadas internas.

Um aplicativo baseado em microsserviços é um sistema distribuído em execução em vários processos ou serviços, geralmente, até mesmo em vários servidores ou hosts. Cada instância de serviço geralmente é um processo. Portanto, os serviços devem interagir usando um protocolo de comunicação entre processos, como HTTP, AMQP ou um protocolo binário, como TCP, dependendo da natureza de cada serviço.

A comunidade de microsserviços promove a filosofia de "[pontos de extremidade inteligentes e pipes tolos](https://simplicable.com/new/smart-endpoints-and-dumb-pipes)" Este slogan incentiva um design o mais desacoplado possível entre os microsserviços e o mais coeso possível dentro de um único microsserviço. Conforme explicado anteriormente, cada microsserviço tem seus próprios dados e sua própria lógica do domínio. Mas os microsserviços que compõem um aplicativo de ponta a ponta geralmente são coreografados simplesmente usando comunicações REST em vez de protocolos complexos, como WS-\*, e comunicações flexíveis controladas por evento, em vez de orquestradores de negócios e processos centralizados.

Os dois protocolos mais usados são solicitação/resposta HTTP com APIs de recurso (principalmente em consultas) e mensagens assíncronas leves, ao comunicar atualizações entre vários microsserviços. Isso será mais bem explicado nas seções a seguir.

## <a name="communication-types"></a>Tipos de comunicação

O cliente e os serviços podem se comunicar por vários tipos de comunicação diferentes, cada um direcionando a um cenário diferente e a metas diferentes. Inicialmente, esses tipos de comunicação podem ser classificados em dois eixos.

O primeiro eixo define se o protocolo é síncrono ou assíncrono:

- Protocolo síncrono. HTTP é um protocolo síncrono. O cliente envia uma solicitação e espera uma resposta do serviço. Isso é independente da execução do código do cliente que pode ser síncrona (o thread é bloqueado) ou assíncrona (o thread não é bloqueado e a resposta acabará alcançando um retorno de chamada). O ponto importante aqui é que o protocolo (HTTP/HTTPS) é síncrono e o código do cliente somente poderá continuar sua tarefa quando receber a resposta do servidor HTTP.

- Protocolo assíncrono. Outros protocolos, como o AMQP (um protocolo compatível com vários sistemas operacionais e ambientes de nuvem), usam mensagens assíncronas. O código do cliente ou o remetente da mensagem geralmente não espera uma resposta. Ele apenas envia a mensagem como ao enviar uma mensagem para uma fila do RabbitMQ ou para qualquer outro agente de mensagens.

O segundo eixo define se a comunicação tem um único destinatário ou vários destinatários:

- Único destinatário. Cada solicitação deve ser processada por exatamente um destinatário ou serviço. Um exemplo dessa comunicação é o [Padrão de comando](https://en.wikipedia.org/wiki/Command_pattern).

- Vários destinatários. Cada solicitação pode ser processada por nenhum destinatário, por um ou por vários destinatários. Esse tipo de comunicação precisa ser assíncrono. Um exemplo é o mecanismo [de publicação/assinatura](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern) usado em padrões como a [Arquitetura orientada por eventos](https://microservices.io/patterns/data/event-driven-architecture.html). Ele se baseia em um agente de mensagem ou em uma interface de barramento de evento ao propagar atualizações de dados entre vários microsserviços por meio de eventos. Ele geralmente é implementado por meio de um barramento de serviço ou artefato semelhante, como o [Barramento de Serviço do Azure](https://azure.microsoft.com/services/service-bus/), usando [tópicos e assinaturas](/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).

Um aplicativo baseado em microsserviço geralmente usará uma combinação desses estilos de comunicação. O tipo mais comum é a comunicação de único destinatário com um protocolo síncrono como HTTP/HTTPS ao invocar um serviço HTTP de API Web regular. Geralmente os microsserviços também usam protocolos de mensagens para a comunicação assíncrona entre eles.

É bom conhecer esses eixos para esclarecer melhor os mecanismos de comunicação possíveis, mas eles não são as questões mais importantes ao criar microsserviços. Não é a natureza assíncrona da execução de thread de cliente nem a natureza assíncrona do protocolo selecionado os pontos mais importantes ao integrar microsserviços. O que *é* importante é ser capaz de integrar os microsserviços de forma assíncrona, mantendo a independência dos microsserviços, conforme será explicado na seção a seguir.

## <a name="asynchronous-microservice-integration-enforces-microservices-autonomy"></a>A integração assíncrona dos microsserviços impõe a autonomia do microsserviço

Conforme mencionado, o ponto importante ao criar um aplicativo baseado em microsserviços é a maneira de integrar os microsserviços. O ideal é tentar minimizar a comunicação entre os microsserviços internos. Quanto menos comunicações entre os microsserviços, melhor. Mas, em muitos casos, será necessário integrar os microsserviços de alguma forma. Quando isso for necessário, a regra crítica será que a comunicação entre os microsserviços deve ser assíncrona. Isso não significa que você precisa usar um protocolo específico (por exemplo, um sistema de mensagens assíncrono em vez de HTTP síncrono). Isso apenas significa que a comunicação entre os microsserviços deve ser feita somente pela propagação de dados de forma assíncrona, mas tente não depender de outros microsserviços internos como parte da operação inicial de solicitação/resposta HTTP do serviço.

Se possível, nunca dependa da comunicação síncrona (solicitação/resposta) entre vários microsserviços, nem mesmo para consultas. O objetivo de cada microsserviço é ser autônomo e estar disponível para o consumidor cliente, mesmo se outros serviços que façam parte do aplicativo de ponta a ponta estiverem inativos ou não íntegros. Se você acha que precisa fazer uma chamada de um microsserviço para outros microsserviços (como executar uma solicitação HTTP para uma consulta de dados) para poder fornecer uma resposta a um aplicativo cliente, você tem uma arquitetura que não será resiliente quando alguns microsserviços falharem.

Além disso, as dependências de HTTP entre os microsserviços, como ao criar longos ciclos de solicitação/resposta com cadeias de solicitação HTTP, como foi mostrado na primeira parte da Figura 4-15, não permitem que os microsserviços sejam autônomos e também afetam o desempenho dos microsserviços quando um dos serviços nessa cadeia não é executado corretamente.

Quanto mais você adicionar dependências síncronas entre os microsserviços, como solicitações de consulta, pior será o tempo de resposta geral para os aplicativos clientes.

![Diagrama mostrando três tipos de comunicação entre os microserviços.](./media/communication-in-microservice-architecture/sync-vs-async-patterns-across-microservices.png)

**Figura 4-15**. Antipadrões e padrões na comunicação entre microsserviços

Conforme mostrado no diagrama acima, na comunicação síncrona, uma "cadeia" de solicitações é criada entre os microserviços enquanto atende à solicitação do cliente. Isso é um antipadrão. Em microsserviços de comunicação assíncrona, use mensagens assíncronas ou a sondagem http para se comunicar com outros microsserviços, mas a solicitação do cliente é atendida imediatamente.

Se seu microsserviço precisar gerar uma ação adicional em outro microsserviço, se possível, não execute essa ação de forma síncrona e como parte da operação original de solicitação e resposta do microsserviço. Nesse caso, faça isso de forma assíncrona (usando o serviço de mensagens assíncrono ou eventos de integração, filas, etc.). No entanto, tanto quanto possível, não invoque a ação de forma síncrona como parte da operação de solicitação e resposta síncrona original.

E, finalmente, (e este é o momento em que maioria dos problemas surgem ao criar microsserviços), se o microsserviço inicial precisar de dados que sejam originalmente pertencentes a outros microsserviços, não confie em fazer solicitações síncronas para esses dados. Nesse caso, replique ou propague esses dados (somente os atributos necessários) para o banco de dados do serviço inicial usando consistência eventual (normalmente com eventos de integração, conforme será explicado nas próximas seções).

Como observado anteriormente nos [limites de modelo de domínio de identificação para cada seção de microserviço](identify-microservice-domain-model-boundaries.md) , duplicar alguns dados em vários microserviços não é um design incorreto — em contrário, ao fazer isso, você pode converter os dados no idioma específico ou nos termos desse domínio adicional ou de contexto limitado. Por exemplo, no [aplicativo eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) , você tem um microserviço chamado `identity-api` que é responsável pela maioria dos dados do usuário com uma entidade denominada `User` . No entanto, quando você precisar armazenar dados sobre o usuário no `Ordering` microserviço, armazene-os como uma entidade diferente denominada `Buyer` . A `Buyer` entidade compartilha a mesma identidade com a `User` entidade original, mas ela pode ter apenas alguns atributos necessários para o `Ordering` domínio e não todo o perfil do usuário.

Você pode usar qualquer protocolo para comunicar e propagar dados de forma assíncrona entre os microsserviços para garantir a consistência eventual. Conforme mencionado, você pode usar eventos de integração com um barramento de evento, com um agente de mensagem ou até mesmo com sondagem HTTP dos outros serviços. Não importa. A regra importante é não criar dependências síncronas entre os microsserviços.

As seções a seguir explicam os vários estilos de comunicação que você pode considerar para um aplicativo baseado em microsserviço.

## <a name="communication-styles"></a>Estilos de comunicação

Existem vários protocolos e opções que você pode usar para comunicação, dependendo do tipo de comunicação que deseja usar. Se você estiver usando um mecanismo de comunicação baseado em solicitação/resposta síncrona, protocolos como HTTP e REST serão os mais comuns, principalmente se você estiver publicando serviços fora do host do Docker ou do cluster de microsserviços. Se você estiver fazendo a comunicação entre serviços internamente (no host do Docker ou no cluster de microsserviços), também será possível usar os mecanismos de comunicação de formato binário (como o WCF usando TCP e o formato binário). Como alternativa, você pode usar mecanismos de comunicação assíncrona baseada em mensagem, como o AMQP.

Também há vários formatos de mensagem como JSON ou XML, ou até mesmo formatos binários, que podem ser mais eficientes. Se o formato binário escolhido não for um padrão, provavelmente, não será uma boa ideia publicar os serviços publicamente usando esse formato. É possível usar um formato não padrão para a comunicação interna entre os microsserviços. Você pode fazer isso na comunicação entre os microsserviços dentro do host do Docker ou do cluster de microsserviços (por exemplo, orquestradores do Docker) ou para aplicativos cliente do proprietário que se comunicam com os microsserviços.

### <a name="requestresponse-communication-with-http-and-rest"></a>Comunicação de solicitação/resposta com HTTP e REST

Quando um cliente usa a comunicação de solicitação/resposta, ele envia uma solicitação para um serviço e, em seguida, o serviço processa a solicitação e retorna uma resposta. A comunicação de solicitação/resposta é muito adequada principalmente para consultar dados de uma interface do usuário em tempo real (uma interface do usuário em tempo real) dos aplicativos clientes. Portanto, em uma arquitetura de microsserviço provavelmente você usará esse mecanismo de comunicação para a maioria das consultas, conforme mostrado na Figura 4-16.

![Diagrama mostrando os comentários de solicitação/resposta para consultas ao vivo e atualizações.](./media/communication-in-microservice-architecture/request-response-comms-live-queries-updates.png)

**Figura 4-16**. Usando a comunicação de solicitação/resposta HTTP (síncrona ou assíncrona)

Quando um cliente usa a comunicação de solicitação/resposta, ele considera que a resposta chegará muito em breve, geralmente, em menos de um segundo ou, no máximo, em alguns segundos. Para respostas em atraso, você precisa implementar a comunicação assíncrona baseada em [padrões de sistema de mensagens](/azure/architecture/patterns/category/messaging) e em [tecnologias de sistema de mensagens](https://en.wikipedia.org/wiki/Message-oriented_middleware), que é uma abordagem diferente que explicaremos na próxima seção.

Um estilo popular de arquitetura para comunicação de solicitação/resposta é o [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) (Transferência de Estado Representacional). Essa abordagem é baseada e fortemente vinculada ao protocolo [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol), adotando verbos HTTP como GET, POST e PUT. O REST é a abordagem de comunicação de arquitetura mais comum usada na criação de serviços. Você pode implementar serviços REST ao desenvolver serviços de API Web ASP.NET Core.

Há um valor adicional ao usar serviços REST HTTP como sua linguagem IDL. Por exemplo, ao usar [metadados do Swagger](https://swagger.io/) para descrever sua API de serviço, você poderá usar ferramentas que geram stubs de cliente para descobrir e consumir seus serviços diretamente.

### <a name="additional-resources"></a>Recursos adicionais

- **Martin Fowler. Modelo de maturidade Richardson** uma descrição do modelo REST. \
  <https://martinfowler.com/articles/richardsonMaturityModel.html>

- **Swagger** O site oficial. \
  <https://swagger.io/>

### <a name="push-and-real-time-communication-based-on-http"></a>Comunicação por push e em tempo real baseada em HTTP

Outra possibilidade (geralmente para finalidades diferentes do REST) é uma comunicação em tempo real e de um-para-muitos com estruturas de nível mais alto, como [ASP.NET SignalR](https://www.asp.net/signalr) e protocolos como [WebSockets](https://en.wikipedia.org/wiki/WebSocket).

Como mostra a Figura 4-17, a comunicação HTTP em tempo real significa que o código do servidor pode enviar conteúdo por push para os clientes conectados à medida que os dados ficam disponíveis, ou seja, o servidor não precisa esperar que um cliente solicite novos dados.

![Diagrama mostrando os comentários de push e em tempo real com base no Signalr.](./media/communication-in-microservice-architecture/one-to-many-communication.png)

**Figura 4-17**. Comunicação de mensagens assíncronas de um para muitos em tempo real

O SignalR é uma boa maneira de atingir a comunicação em tempo real para enviar por push o conteúdo para os clientes de um servidor de back-end. Como a comunicação ocorre em tempo real, os aplicativos clientes mostram as alterações quase instantaneamente. Geralmente, isso é tratado por um protocolo como WebSockets, usando várias conexões de WebSocket (uma por cliente). Um exemplo típico é quando um serviço comunica uma alteração na pontuação de um jogo de esportes para vários aplicativos Web clientes simultaneamente.

>[!div class="step-by-step"]
>[Anterior](direct-client-to-microservice-communication-versus-the-api-gateway-pattern.md) 
> [Avançar](asynchronous-message-based-communication.md)
