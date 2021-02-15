---
title: Comunicação entre serviços
description: Saiba como os microserviços nativos de nuvem de back-end se comunicam com outros microserviços de back-end.
author: robvet
ms.date: 01/19/2021
ms.openlocfilehash: 63c80b38e2fa42dccebefc772c969266fa9d79ca
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506260"
---
# <a name="service-to-service-communication"></a>Comunicação entre serviços

Mudando do cliente front-end, agora resolvemos que os microserviços de back-end se comunicam entre si.

Ao construir um aplicativo nativo de nuvem, você desejará ser sensível à forma como os serviços de back-end se comunicam entre si. Idealmente, quanto menos comunicação entre serviços, melhor. No entanto, evitar nem sempre é possível, pois os serviços de back-end muitas vezes dependem uns dos outros para concluir uma operação.

Há várias abordagens amplamente aceitas para implementar a comunicação entre serviços. O *tipo de interação de comunicação* geralmente determinará a melhor abordagem.

Considere os seguintes tipos de interação:

- *Consulta* – quando um microserviço de chamada requer uma resposta de um Microservice chamado, como "Ei, forneça as informações do comprador para uma determinada ID do cliente".

- *Comando* – quando o microserviço de chamada precisa de outro microserviço para executar uma ação, mas não requer uma resposta, como "Ei, apenas envia este pedido."

- *Evento* – quando um microserviço, chamado de Publicador, gera um evento que o estado mudou ou uma ação ocorreu. Outros microserviços, chamados assinantes, que estão interessados, podem reagir ao evento adequadamente. O Publicador e os assinantes não estão cientes uns dos outros.

Os sistemas de microserviço normalmente usam uma combinação desses tipos de interação ao executar operações que exigem interação entre serviços. Vamos examinar cada um e saber como você pode implementá-los.

## <a name="queries"></a>Consultas

Muitas vezes, um microserviço pode precisar *consultar* outro, exigindo uma resposta imediata para concluir uma operação. Um microserviço da cesta de compras pode precisar de informações do produto e um preço para adicionar um item à sua cesta. Há muitas abordagens para implementar operações de consulta.

### <a name="requestresponse-messaging"></a>Mensagens de solicitação/resposta

Uma opção para implementar esse cenário é que o microserviço de back-end de chamada faça solicitações HTTP diretas para os microserviços que precisa consultar, mostrados na Figura 4-8.

![Comunicação direta de HTTP](./media/direct-http-communication.png)

**Figura 4-8**. Comunicação direta de HTTP

Embora as chamadas HTTP diretas entre os microserviços sejam relativamente simples de implementar, deve-se ter cuidado para minimizar essa prática. Para começar, essas chamadas são sempre *síncronas* e bloquearão a operação até que um resultado seja retornado ou a solicitação atingir o tempo limite. O que era um pouco independente, os serviços independentes, capazes de evoluir de forma independente e implantar com frequência, agora são acoplados entre si. Como o acoplamento entre os microserviços aumenta, seus benefícios arquitetônicos diminuem.

A execução de uma solicitação infrequente que faz uma única chamada HTTP direta para outro microserviço pode ser aceitável para alguns sistemas. No entanto, chamadas de alto volume que invocam chamadas HTTP diretas para vários microserviços não são aconselhadas. Eles podem aumentar a latência e afetar negativamente o desempenho, a escalabilidade e a disponibilidade do seu sistema. Ainda pior, uma longa série de comunicação HTTP direta pode levar a cadeias profundas e complexas de chamadas de microservices síncronas, mostradas na Figura 4-9:

![Encadeando consultas HTTP](./media/chaining-http-queries.png)

**Figura 4-9**. Encadeando consultas HTTP

Certamente, você pode imaginar o risco no design mostrado na imagem anterior. O que acontece se a etapa \# 3 falhar? Ou a etapa \# 8 falha? Como você se recupera? E se \# a etapa 6 estiver lenta porque o serviço subjacente está ocupado? Como você continua? Mesmo que tudo funcione corretamente, considere a latência que essa chamada incorreria, que é a soma da latência de cada etapa.

O grande grau de acoplamento na imagem anterior sugere que os serviços não foram modelados de forma ideal. Seria cabe a equipe a revisitar seu design.

### <a name="materialized-view-pattern"></a>Padrão de Exibição Materializada

Uma opção popular para remover o acoplamento de microatendimento é o [padrão de exibição materializado](/azure/architecture/patterns/materialized-view). Com esse padrão, um microserviço armazena sua própria cópia local e desnormalizada dos dados pertencentes a outros serviços. Em vez do microserviço da cesta de compras consultar o catálogo de produtos e os microserviços, ele mantém sua própria cópia local desses dados. Esse padrão elimina o acoplamento desnecessário e melhora a confiabilidade e o tempo de resposta. A operação inteira é executada dentro de um único processo. Exploramos esse padrão e outras preocupações de dados no capítulo 5.

### <a name="service-aggregator-pattern"></a>Padrão de agregador de serviço

Outra opção para eliminar o acoplamento de microserviço para microserviço é um [microserviço agregador](https://devblogs.microsoft.com/cesardelatorre/designing-and-implementing-api-gateways-with-ocelot-in-a-microservices-and-container-based-architecture/), mostrado em roxo na Figura 4-10.

![Serviço de agregador](./media/aggregator-service.png)

**Figura 4-10**. Microserviço agregador

O padrão Isola uma operação que faz chamadas para vários microserviços de back-end, centralizando sua lógica em um microserviço especializado.  O microserviço agregador de check-out roxo na figura anterior orquestra o fluxo de trabalho para a operação de check-out. Ele inclui chamadas para vários microserviços de back-end em uma ordem sequenciada. Os dados do fluxo de trabalho são agregados e retornados ao chamador. Embora ainda implemente chamadas HTTP diretas, o microserviço de agregador reduz as dependências diretas entre os microserviços de back-end.

### <a name="requestreply-pattern"></a>Padrão de solicitação/resposta

Outra abordagem para desacoplar mensagens HTTP síncronas é um [padrão de solicitação-resposta](https://www.enterpriseintegrationpatterns.com/patterns/messaging/RequestReply.html), que usa a comunicação de enfileiramento. A comunicação usando uma fila é sempre um canal unidirecional, com um produtor enviando a mensagem e o consumidor recebendo-a. Com esse padrão, uma fila de solicitação e uma fila de resposta são implementadas, mostradas na Figura 4-11.

![Padrão de solicitação-resposta](./media/request-reply-pattern.png)

**Figura 4-11**. Padrão de solicitação-resposta

Aqui, o produtor da mensagem cria uma mensagem baseada em consulta que contém uma ID de correlação exclusiva e a coloca em uma fila de solicitação. O serviço de consumo removerá as mensagens da fila, processará e colocará a resposta na fila de respostas com a mesma ID de correlação. O serviço produtor removerá a mensagem da fila, a corresponderá com a ID de correlação e continuará o processamento. Abordaremos as filas detalhadamente na próxima seção.

## <a name="commands"></a>Comandos

Outro tipo de interação de comunicação é um *comando*. Um microserviço pode precisar de outro microserviço para executar uma ação. O microserviço de pedidos pode precisar do microserviço de envio para criar uma remessa para uma ordem aprovada. Na Figura 4-12, um microserviço, chamado produtor, envia uma mensagem para outro microserviço, o consumidor, o comando para fazer algo.

![Interação do comando com uma fila](./media/command-interaction-with-queue.png)

**Figura 4-12**. Interação do comando com uma fila

Geralmente, o produtor não requer uma resposta e pode *acionar e esquecer* a mensagem. Se uma resposta for necessária, o consumidor enviará uma mensagem separada de volta para o produtor em outro canal. Uma mensagem de comando é melhor enviada de forma assíncrona com uma fila de mensagens. com suporte de um agente de mensagem leve. No diagrama anterior, observe como uma fila separa e dissocia os dois serviços.

Uma fila de mensagens é uma construção intermediária por meio da qual um produtor e um consumidor passam uma mensagem. As filas implementam um padrão de mensagens assíncronas de ponto a ponto. O produtor sabe onde um comando precisa ser enviado e direcionado adequadamente. A fila garante que uma mensagem seja processada por exatamente uma das instâncias de consumidor que estão sendo lidas do canal. Nesse cenário, o produtor ou o serviço de consumidor pode escalar horizontalmente sem afetar o outro. Além disso, as tecnologias podem ser diferentes em cada lado, o que significa que poderemos ter um microserviço Java chamando um microserviço do [Golang](https://golang.org) .

No capítulo 1, falamos sobre os *serviços de backup*. Os serviços de backup são recursos complementares dos quais os sistemas nativos de nuvem dependem. As filas de mensagens estão fazendo serviços de backup. A nuvem do Azure dá suporte a dois tipos de filas de mensagens que seus sistemas nativos de nuvem podem consumir para implementar mensagens de comando: filas do armazenamento do Azure e filas do barramento de serviço do Azure.

### <a name="azure-storage-queues"></a>Filas de Armazenamento do Azure

As filas do armazenamento do Azure oferecem uma infraestrutura de fila simples que é rápida, acessível e apoiada pelas contas de armazenamento do Azure.

As [filas do armazenamento do Azure](/azure/storage/queues/storage-queues-introduction) apresentam um mecanismo de enfileiramento baseado em REST com mensagens confiáveis e persistentes. Eles fornecem um conjunto mínimo de recursos, mas são baratos e armazenam milhões de mensagens. Sua capacidade varia até 500 TB. Uma única mensagem pode ter até 64 KB de tamanho.

Você pode acessar mensagens de qualquer lugar do mundo por meio de chamadas autenticadas usando HTTP ou HTTPS. As filas de armazenamento podem ser expandidas para um grande número de clientes simultâneos para lidar com picos de tráfego.

Dito isso, há limitações com o serviço:

- A ordem da mensagem não é garantida.

- Uma mensagem só pode persistir por sete dias antes de ser removida automaticamente.

- O suporte para gerenciamento de estado, detecção de duplicidades ou transações não está disponível.

A Figura 4-13 mostra a hierarquia de uma fila de armazenamento do Azure.

![Hierarquia da fila de armazenamento](./media/storage-queue-hierarchy.png)

**Figura 4-13**. Hierarquia da fila de armazenamento

Na figura anterior, observe como as filas de armazenamento armazenam suas mensagens na conta de armazenamento do Azure subjacente.

Para desenvolvedores, a Microsoft fornece várias bibliotecas do cliente e do lado do servidor para o processamento da fila de armazenamento. Há suporte para a maioria das principais plataformas, incluindo .NET, Java, JavaScript, Ruby, Python e go. Os desenvolvedores nunca devem se comunicar diretamente com essas bibliotecas. Isso irá acoplar rigidamente o código de seu microserviço ao serviço Fila de armazenamento do Azure. É uma prática melhor isolar os detalhes de implementação da API. Introduza uma camada de intermediação ou uma API intermediária, que expõe operações genéricas e encapsula a biblioteca concreta. Esse acoplamento flexível permite que você troque um serviço de enfileiramento para outro sem precisar fazer alterações no código de serviço principal.

As filas do armazenamento do Azure são uma opção econômica para implementar mensagens de comando em seus aplicativos nativos de nuvem. Especialmente quando um tamanho de fila exceder 80 GB ou um conjunto de recursos simples é aceitável. Você paga apenas pelo armazenamento das mensagens; Não há encargos fixos por hora.

### <a name="azure-service-bus-queues"></a>Filas do Barramento de Serviço do Azure

Para requisitos de mensagens mais complexos, considere as filas do barramento de serviço do Azure.

Sentado em uma infra-estrutura de mensagens robusta, o [barramento de serviço do Azure](/azure/service-bus-messaging/service-bus-messaging-overview) dá suporte a um *modelo de mensagens orientadas*. As mensagens são armazenadas de forma confiável em um agente (a fila) até serem recebidas pelo consumidor. A fila garante a entrega de mensagem PEPS (primeiro a entrar/primeiro a sair), respeitando a ordem na qual as mensagens foram adicionadas à fila.

O tamanho de uma mensagem pode ser muito maior, até 256 KB. As mensagens são mantidas na fila por um período de tempo ilimitado. O barramento de serviço dá suporte a chamadas não apenas baseadas em HTTP, mas também fornece suporte completo para o [protocolo AMQP](/azure/service-bus-messaging/service-bus-amqp-overview). O AMQP é um padrão aberto entre os fornecedores que oferece suporte a um protocolo binário e a níveis mais altos de confiabilidade.

O barramento de serviço fornece um conjunto avançado de recursos, incluindo [suporte a transações](/azure/service-bus-messaging/service-bus-transactions) e um recurso de [detecção de duplicidades](/azure/service-bus-messaging/duplicate-detection). A fila garante "no máximo uma vez na entrega" por mensagem. Ele descarta automaticamente uma mensagem que já foi enviada. Se um produtor estiver em dúvida, ele poderá reenviar a mesma mensagem, e o barramento de serviço garante que apenas uma cópia será processada. A detecção de duplicidades libera você de ter que criar o direcionamento de infraestrutura adicional.

Mais dois recursos corporativos são particionamento e sessões. Uma fila convencional do barramento de serviço é tratada por um único agente de mensagem e armazenada em um único repositório de mensagens. Mas, o [particionamento do barramento de serviço](/azure/service-bus-messaging/service-bus-partitioning) espalha a fila entre vários agentes de mensagens e repositórios de mensagens. A taxa de transferência geral não é mais limitada pelo desempenho de um único agente de mensagens ou repositório de mensagens. Uma interrupção temporária de um repositório de mensagens não torna uma fila particionada indisponível.

As [sessões do barramento de serviço](https://codingcanvas.com/azure-service-bus-sessions/) fornecem uma maneira de agrupar mensagens relacionadas. Imagine um cenário de fluxo de trabalho em que as mensagens devem ser processadas em conjunto e a operação seja concluída no final. Para tirar proveito, as sessões devem ser explicitamente habilitadas para a fila e cada mensagem relacionada deve conter a mesma ID de sessão.

No entanto, há algumas advertências importantes: o tamanho das filas do barramento de serviço é limitado a 80 GB, o que é muito menor do que o que está disponível nas filas de armazenamento. Além disso, as filas do barramento de serviço incorrem em custo base e cobrança por operação.

A Figura 4-14 descreve a arquitetura de alto nível de uma fila do barramento de serviço.

![Fila do Barramento de Serviço](./media/service-bus-queue.png)

**Figura 4-14**. Fila do Barramento de Serviço

Na figura anterior, observe a relação ponto a ponto. Duas instâncias do mesmo provedor estão enfileirando mensagens em uma única fila do barramento de serviço. Cada mensagem é consumida por apenas uma das três instâncias de consumidor à direita. Em seguida, discutiremos como implementar mensagens em que diferentes consumidores podem estar interessados na mesma mensagem.

## <a name="events"></a>Eventos

O enfileiramento de mensagens é uma maneira eficaz de implementar a comunicação em que um produtor pode enviar uma mensagem por um consumidor de forma assíncrona. No entanto, o que acontece quando *muitos consumidores diferentes* estão interessados na mesma mensagem? Uma fila de mensagens dedicada para cada consumidor não pode ser bem dimensionada e seria difícil de gerenciar.

Para resolver esse cenário, mudamos para o terceiro tipo de interação de mensagem, o *evento*. Um microserviço anuncia que uma ação ocorreu. Outros microserviços, se estiverem interessados, reagir à ação ou ao evento.

O evento é um processo de duas etapas. Para uma determinada alteração de estado, um microserviço publica um evento em um agente de mensagem, disponibilizando-o para qualquer outro microserviço interessado. O microserviço interessado é notificado pela assinatura do evento no agente de mensagens. Você usa o padrão de [publicação/assinatura](/azure/architecture/patterns/publisher-subscriber) para implementar a [comunicação baseada em eventos](/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/integration-event-based-microservice-communications).

A Figura 4-15 mostra um microserviço de cesta de compras publicando um evento com dois outros microservices assinando-o.

![Event-Driven mensagens](./media/event-driven-messaging.png)

**Figura 4-15**. Event-Driven mensagens

Observe o componente de *barramento de evento* que fica no meio do canal de comunicação. É uma classe personalizada que encapsula o agente de mensagem e o dissocia do aplicativo subjacente. Os microserviços de pedidos e de inventário operam de forma independente o evento sem nenhum conhecimento um do outro, nem o microserviço da cesta de compras. Quando o evento registrado é publicado no barramento de evento, eles agem sobre ele.

Com eventos, mudamos da tecnologia de enfileiramento para *Tópicos*. Um [tópico](/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions) é semelhante a uma fila, mas dá suporte a um padrão de mensagens de um-para-muitos. Um microserviço publica uma mensagem. Vários microserviços de assinatura podem optar por receber e agir sobre essa mensagem. A Figura 4-16 mostra uma arquitetura de tópico.

![Arquitetura do tópico](./media/topic-architecture.png)

**Figura 4-16**. Arquitetura do tópico

Na figura anterior, os editores enviam mensagens para o tópico. No final, os assinantes recebem mensagens de assinaturas. No meio, o tópico encaminha mensagens para assinaturas com base em um conjunto de regras, mostrado em caixas azuis escuras. As regras atuam como um filtro que encaminha mensagens específicas para uma assinatura. Aqui, um evento "getPrice" seria enviado para as assinaturas Price e logging, pois a assinatura de log optou por receber todas as mensagens.  Um evento "GetInformation" seria enviado para as informações e assinaturas de registro em log.

A nuvem do Azure dá suporte a dois serviços de tópico diferentes: tópicos do barramento de serviço do Azure e EventGrid do Azure.

### <a name="azure-service-bus-topics"></a>Tópicos do Barramento de Serviço do Azure

A parte superior do mesmo modelo robusto de mensagens orientadas das filas do barramento de serviço do Azure são os [Tópicos do barramento de serviço do Azure](/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions). Um tópico pode receber mensagens de vários Publicadores independentes e enviar mensagens para até 2.000 assinantes. As assinaturas podem ser adicionadas ou removidas dinamicamente no tempo de execução sem interromper o sistema ou recriar o tópico.

Muitos recursos avançados das filas do barramento de serviço do Azure também estão disponíveis para tópicos, incluindo [detecção de duplicidades](/azure/service-bus-messaging/duplicate-detection) e [suporte a transações](/azure/service-bus-messaging/service-bus-transactions). Por padrão, os tópicos do barramento de serviço são tratados por um único agente de mensagem e armazenados em um único repositório de mensagens. Mas, o [particionamento do barramento de serviço](/azure/service-bus-messaging/service-bus-partitioning) dimensiona um tópico distribuindo-o em vários agentes de mensagens e armazenamentos de mensagens.

A [entrega de mensagem agendada](/azure/service-bus-messaging/message-sequencing) marca uma mensagem com um horário específico para processamento. A mensagem não aparecerá no tópico antes dessa hora. O [adiamento de mensagens](/azure/service-bus-messaging/message-deferral) permite adiar uma recuperação de uma mensagem para um momento posterior. Ambos são comumente usados em cenários de processamento de fluxo de trabalho em que as operações são processadas em uma ordem específica. Você pode adiar o processamento de mensagens recebidas até que o trabalho anterior tenha sido concluído.

Os tópicos do barramento de serviço são uma tecnologia robusta e comprovada para habilitar a comunicação de publicação/assinatura em seus sistemas nativos de nuvem.

### <a name="azure-event-grid"></a>Grade de Eventos do Azure

Embora o barramento de serviço do Azure seja um agente de mensagens testado por batalha com um conjunto completo de recursos corporativos, a [grade de eventos do Azure](/azure/event-grid/overview) é a nova criança no bloco.

À primeira vista, a grade de eventos pode parecer apenas com outro sistema de mensagens baseado em tópico. No entanto, ele é diferente de várias maneiras. Focado em cargas de trabalho controladas por eventos, ele permite o processamento de eventos em tempo real, a profunda integração do Azure e uma plataforma aberta em uma infraestrutura sem servidor. Ele foi projetado para aplicativos contemporâneos de nuvem e nativas para servidores

Como um *replano de evento* centralizado, ou pipe, a grade de eventos reage a eventos dentro dos recursos do Azure e de seus próprios serviços.

As notificações de eventos são publicadas em um tópico da grade de eventos que, por sua vez, roteia cada evento para uma assinatura. Os assinantes mapeiam para assinaturas e consomem os eventos. Assim como o barramento de serviço, a grade de eventos dá suporte a um *modelo de assinante filtrado* em que uma assinatura define a regra para os eventos que deseja receber. A grade de eventos fornece uma taxa de transferência rápida com uma garantia de 10 milhões eventos por segundo, permitindo entrega quase em tempo real – muito mais do que o barramento de serviço do Azure pode gerar.

Um ponto ideal para a grade de eventos é sua integração profunda com a malha da infraestrutura do Azure. Um recurso do Azure, como o Cosmos DB, pode publicar eventos internos diretamente em outros recursos interessados do Azure, sem a necessidade de código personalizado. A grade de eventos pode publicar eventos de uma assinatura do Azure, grupo de recursos ou serviço, proporcionando aos desenvolvedores um controle refinado sobre o ciclo de vida dos recursos de nuvem. No entanto, a grade de eventos não está limitada ao Azure. É uma plataforma aberta que pode consumir eventos HTTP personalizados publicados de aplicativos ou serviços de terceiros e rotear eventos para assinantes externos.

Ao publicar e assinar eventos nativos de recursos do Azure, nenhuma codificação é necessária. Com a configuração simples, você pode integrar eventos de um recurso do Azure para outro, aproveitando o direcionamento interno para tópicos e assinaturas. A Figura 4-17 mostra a anatomia da grade de eventos.

![Anatomia da grade de eventos](./media/event-grid-anatomy.png)

**Figura 4-17**. Anatomia da grade de eventos

Uma grande diferença entre o EventGrid e o barramento de serviço é o *padrão de troca de mensagens* subjacente.

O barramento de serviço implementa um *modelo de pull* de estilo mais antigo no qual o assinante downstream sonda ativamente a assinatura do tópico em busca de novas mensagens. Na cabeça, essa abordagem dá ao Assinante controle total do ritmo no qual ele processa as mensagens. Ele controla quando e quantas mensagens são processadas em um determinado momento. As mensagens não lidas permanecem na assinatura até que sejam processadas. Uma deficiência significativa é a latência entre a hora em que o evento é gerado e a operação de sondagem que efetua pull dessa mensagem para o Assinante para processamento. Além disso, a sobrecarga de sondagem constante para o próximo evento consome recursos e dinheiro.

EventGrid, no entanto, é diferente. Ele implementa um *modelo de push* no qual os eventos são enviados para os EventHandlers como recebidos, fornecendo entrega de eventos quase em tempo real. Ele também reduz o custo, pois o serviço é disparado apenas quando é necessário consumir um evento – não continuamente, assim como acontece com a sondagem. Dito isso, um manipulador de eventos deve lidar com a carga de entrada e fornecer mecanismos de limitação para se proteger contra sobrecarregar. Muitos serviços do Azure que consomem esses eventos, como Azure Functions e aplicativos lógicos, fornecem recursos automáticos de AutoEscala para lidar com cargas maiores.  

A grade de eventos é um serviço de nuvem sem servidor totalmente gerenciado. Ele é dimensionado dinamicamente com base no seu tráfego e cobra você apenas pelo uso real, não pela capacidade adquirida previamente. As primeiras 100.000 operações por mês são gratuitas – operações que estão sendo definidas como entrada de evento (notificações de eventos de entrada), tentativas de entrega de assinatura, chamadas de gerenciamento e filtragem por assunto. Com a disponibilidade de 99,99%, o EventGrid garante a entrega de um evento dentro de um período de 24 horas, com funcionalidade de repetição interna para entrega sem êxito. As mensagens não entregues podem ser movidas para uma fila de "mensagens mortas" para resolução.  Ao contrário do barramento de serviço do Azure, a grade de eventos é ajustada para desempenho rápido e não oferece suporte a recursos como mensagens ordenadas, transações e sessões.

### <a name="streaming-messages-in-the-azure-cloud"></a>Transmissão de mensagens na nuvem do Azure

O barramento de serviço do Azure e a grade de eventos fornecem excelente suporte para aplicativos que expõem eventos únicos e discretos como um novo documento inserido em um Cosmos DB. Mas e se o seu sistema nativo de nuvem precisar processar um *fluxo de eventos relacionados*? Os [fluxos de eventos](/archive/msdn-magazine/2015/february/microsoft-azure-the-rise-of-event-stream-oriented-systems) são mais complexos. Normalmente, eles são ordenados por tempo, inter-relacionados e devem ser processados como um grupo.

O [Hub de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) é uma plataforma de streaming de dados e um serviço de ingestão de eventos que coleta, transforma e armazena eventos. Ele é ajustado para capturar dados de streaming, como notificações de eventos contínuos emitidas de um contexto de telemetria. O serviço é altamente escalonável e pode armazenar e [processar milhões de eventos por segundo](/azure/event-hubs/event-hubs-about). Mostrado na Figura 4-18, geralmente é uma porta frontal para um pipeline de eventos, desacoplando o fluxo de ingestão do consumo de eventos.

![Hub de Eventos do Azure](./media/azure-event-hub.png)

**Figura 4-18**. Hub de Eventos do Azure

O Hub de eventos dá suporte à baixa latência e à retenção de tempo configurável. Ao contrário das filas e dos tópicos, os hubs de eventos mantêm os dados do evento depois que eles são lidos por um consumidor. Esse recurso permite que outros serviços analíticos de dados, internos e externos, reproduza os dados para análise posterior. Os eventos armazenados no Hub de eventos são excluídos somente após a expiração do período de retenção, que é um dia por padrão, mas configurável.

O Hub de eventos dá suporte a protocolos comuns de publicação de eventos, incluindo HTTPS e AMQP. Ele também dá suporte a Kafka 1,0. Os [aplicativos Kafka existentes podem se comunicar com o Hub de eventos](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview) usando o protocolo Kafka, fornecendo uma alternativa ao gerenciamento de clusters grandes do Kafka. Muitos sistemas de código aberto em nuvem nativas adotam o Kafka.

Os hubs de eventos implementam o streaming de mensagens por meio de um [modelo de consumidor particionado](/azure/event-hubs/event-hubs-features) no qual cada consumidor lê apenas um subconjunto específico, ou partição, do fluxo de mensagens. Esse padrão permite a enorme escala horizontal para processamento de eventos e fornece outros recursos centrados no fluxo que não estão disponíveis em filas e tópicos. Uma partição é uma sequência ordenada de eventos que é mantida em um hub de eventos. À medida que novos eventos chegam, eles são adicionados ao final dessa sequência. A Figura 4-19 mostra o particionamento em um hub de eventos.

![Particionamento do hub de eventos](./media/event-hub-partitioning.png)

**Figura 4-19**. Particionamento do hub de eventos

Em vez de ler do mesmo recurso, cada grupo de consumidores lê em um subconjunto, ou partição, do fluxo de mensagens.

Para aplicativos nativos de nuvem que devem transmitir um grande número de eventos, o Hub de eventos do Azure pode ser uma solução robusta e acessível.

>[!div class="step-by-step"]
>[Anterior](front-end-communication.md) 
> [Avançar](grpc.md)
