---
title: Exemplos de design sem servidor-aplicativos sem servidor
description: Entenda a variedade de cenários com suporte de arquiteturas sem servidor, do agendamento e do processamento baseado em evento até gatilhos de arquivo e processo de fluxo.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 3aa9b7951fd8f11a65a64c22443de7041aba7d94
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171748"
---
# <a name="serverless-design-examples"></a>Exemplos de design sem servidor

Há muitos padrões de design que existem para servidores. Esta seção captura alguns cenários comuns que usam sem servidor. O que todos os exemplos têm em comum é a combinação fundamental de um gatilho de evento e lógica de negócios.

## <a name="scheduling"></a>Agendamento

O agendamento de tarefas é uma função comum. O diagrama a seguir mostra um banco de dados herdado que não tem verificações de integridade apropriadas. O banco de dados deve ser limpo periodicamente. A função sem servidor localiza dados inválidos e limpa-os. O gatilho é um temporizador que executa o código em um agendamento.

![Agendamento sem servidor](./media/serverless-scheduling.png)

## <a name="command-and-query-responsibility-segregation-cqrs"></a>Comando e segregação de responsabilidade de consulta (CQRS)

Separação das Operações de Comando e de Consulta (CQRS) é um padrão que fornece diferentes interfaces para leitura (ou consulta) de dados e operações que modificam dados. Ele aborda vários problemas comuns. Em sistemas baseados em criação de atualização de leitura tradicionais (CRUD), os conflitos podem surgir de alto volume de leituras e gravações no mesmo armazenamento de dados. O bloqueio pode ocorrer com frequência e diminui consideravelmente as leituras. Geralmente, os dados são apresentados como uma composição de vários objetos de domínio e as operações de leitura devem combinar dados de entidades diferentes.

Usando o CQRS, uma leitura pode envolver uma entidade "achatada" especial que modela os dados da maneira como eles são consumidos. A leitura é tratada de forma diferente do que é armazenada. Por exemplo, embora o banco de dados possa armazenar um contato como um registro de cabeçalho com um registro de endereço filho, a leitura pode envolver uma entidade com as propriedades de cabeçalho e endereço. Há inúmeras abordagens para criar o modelo de leitura. Pode ser materializado de exibições. As operações de atualização podem ser encapsuladas como eventos isolados que disparam atualizações para dois modelos diferentes. Existem modelos separados para leitura e gravação.

![Exemplo de CQRS](./media/cqrs-example.png)

Sem servidor pode acomodar o padrão CQRS fornecendo os pontos de extremidade segregáveis. Uma função sem servidor acomoda consultas ou leituras e uma função sem servidor ou um conjunto de funções diferente controla as operações de atualização. Uma função sem servidor também pode ser responsável por manter o modelo de leitura atualizado e pode ser disparado pelo [feed de alterações](/azure/cosmos-db/change-feed)do banco de dados. O desenvolvimento de front-end é simplificado para se conectar aos pontos de extremidade necessários. O processamento de eventos é tratado no back-end. Esse modelo também é bem dimensionado para projetos grandes porque diferentes equipes podem trabalhar em operações diferentes.

## <a name="event-based-processing"></a>Processamento baseado em evento

Em sistemas baseados em mensagens, os eventos são frequentemente coletados em filas ou tópicos de Publicador/Assinante para serem afetados. Esses eventos podem disparar funções sem servidor para executar uma parte da lógica de negócios. Um exemplo de processamento baseado em evento são sistemas de origem de eventos. Um "evento" é gerado para marcar uma tarefa como concluída. Uma função sem servidor disparada pelo evento atualiza o documento de banco de dados apropriado. Uma segunda função sem servidor pode usar o evento para atualizar o modelo de leitura para o sistema. A [grade de eventos do Azure](/azure/event-grid/overview) fornece uma maneira de integrar eventos com funções como assinantes.

> Os eventos são mensagens informativas. Para obter mais informações, consulte [padrão de fornecimento de evento](/azure/architecture/patterns/event-sourcing).

## <a name="file-triggers-and-transformations"></a>Gatilhos e transformações de arquivo

Extração, transformação e carregamento (ETL) é uma função comercial comum. Sem servidor é uma ótima solução para ETL porque permite que o código seja disparado como parte de um pipeline. Os componentes de código individuais podem abordar vários aspectos. Uma função sem servidor pode baixar o arquivo, outro aplica a transformação e outro carrega os dados. O código pode ser testado e implantado de forma independente, facilitando a manutenção e a escala onde for necessário.

![Gatilhos e transformações de arquivo sem servidor](./media/serverless-file-triggers.png)

No diagrama, "armazenamento frio" fornece dados analisados em [Azure Stream Analytics](/azure/stream-analytics). Quaisquer problemas encontrados no fluxo de dados disparam uma função do Azure para resolver a anomalia.

## <a name="asynchronous-background-processing-and-messaging"></a>Processamento e mensagens assíncronos em segundo plano

O processamento de mensagens assíncronas e de segundo plano permite que os aplicativos iniciem processos sem precisar esperar. Um exemplo de processamento assíncrono é um aplicativo de OCR. Uma imagem é enviada e enfileirada para processamento. A verificação da imagem para extrair o texto pode levar tempo e, após ser concluída, uma notificação é enviada. Sem servidor pode lidar com a invocação e o resultado nesse cenário.

## <a name="web-apps-and-apis"></a>APIs e aplicativos Web

Um cenário popular para servidores são aplicativos de N camadas, geralmente aqueles em que a camada de interface do usuário é um aplicativo Web. A popularidade dos aplicativos de página única (SPA) aumentou recentemente. Os aplicativos SPA renderizam uma única página e, em seguida, dependem de chamadas à API e dos dados retornados para processar dinamicamente a nova interface do usuário sem recarregar uma página inteira. A renderização do lado do cliente fornece um aplicativo muito mais rápido e responsivo para o usuário final.

Pontos de extremidade sem servidor disparados por chamadas HTTP podem ser usados para lidar com as solicitações de API. Por exemplo, uma empresa de serviços do AD pode chamar uma função sem servidor com informações de perfil do usuário para solicitar publicidade personalizada. A função sem servidor retorna o anúncio personalizado e a página da Web o renderiza.

![API Web sem servidor](./media/serverless-web-api.png)

## <a name="data-pipeline"></a>Pipeline de dados

Funções sem servidor podem ser usadas para facilitar um pipeline de dados. Neste exemplo, um arquivo dispara uma função para converter dados em um arquivo CSV em linhas de dados em uma tabela. A tabela organizada permite que um painel de Power BI apresente a análise ao usuário final.

![Pipeline de dados sem servidor](./media/serverless-data-pipeline.png)

## <a name="stream-processing"></a>Processamento de fluxo

Os dispositivos e sensores geralmente geram fluxos de dados que devem ser processados em tempo real. Há várias tecnologias que podem capturar mensagens e fluxos de [hubs de eventos](/azure/event-hubs/event-hubs-what-is-event-hubs) e [Hub IOT](/azure/iot-hub) para o [barramento de serviço](/azure/service-bus). Independentemente do transporte, o servidor é um mecanismo ideal para processar as mensagens e os fluxos de dados conforme eles chegam. O sem servidor pode ser dimensionado rapidamente para atender à demanda de grandes volumes de dados. O código sem servidor pode aplicar a lógica de negócios para analisar os dados e a saída em um formato estruturado para ação e análise.

![Processamento de fluxo sem servidor](./media/serverless-stream-processing.png)

## <a name="api-gateway"></a>Gateway de API

Um gateway de API fornece um ponto único de entrada para clientes e, em seguida, roteia solicitações de forma inteligente para serviços de back-end. É útil gerenciar grandes conjuntos de serviços. Ele também pode lidar com controle de versão e simplificar o desenvolvimento, conectando facilmente clientes a ambientes diferentes. Sem servidor pode lidar com o dimensionamento de back-end de microservices individuais ao mesmo tempo em que apresenta um único front-end por meio de um gateway de API.

![Gateway de API sem servidor](./media/serverless-api-gateway.png)

## <a name="recommended-resources"></a>Recursos recomendados

- [Grade de Eventos do Azure](/azure/event-grid/overview)
- [Hub IoT do Azure](/azure/iot-hub)
- [Desafios e soluções do gerenciamento de dados distribuídos](../microservices/architect-microservice-container-applications/distributed-data-management.md)
- [Criando microserviços: identificando limites de microatendimento](/azure/architecture/microservices/microservice-boundaries)
- [Hubs de Evento](/azure/event-hubs/event-hubs-what-is-event-hubs)
- [Padrão de fornecimento do evento](/azure/architecture/patterns/event-sourcing)
- [Implementando o padrão de Disjuntor](../microservices/implement-resilient-applications/implement-circuit-breaker-pattern.md)
- [Hub IoT](/azure/iot-hub)
- [Barramento de Serviço](/azure/service-bus)
- [Trabalhando com o suporte ao feed de alterações no Azure Cosmos DB](/azure/cosmos-db/change-feed)

>[!div class="step-by-step"]
>[Anterior](serverless-architecture-considerations.md) 
> [Avançar](azure-serverless-platform.md)
