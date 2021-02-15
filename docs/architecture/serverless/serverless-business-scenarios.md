---
title: Cenários de negócios de exemplo e casos de uso para aplicativos sem servidor
description: Aprenda sem servidor com uma abordagem prática acessando exemplos que variam desde o processamento de imagens até o suporte móvel e pipelines de ETL.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 04/17/2020
ms.openlocfilehash: df76b132579eb3a6d05ce38c94cb9fceb9281aef
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171605"
---
# <a name="serverless-business-scenarios-and-use-cases"></a>Casos de uso e cenários de negócios sem servidor

Há muitos casos de uso e cenários para aplicativos sem servidor. Este capítulo inclui exemplos que ilustram os diferentes cenários. Os cenários incluem links para documentação relacionada e repositórios de código-fonte público. Os exemplos neste capítulo permitem que você comece a usar sua própria compilação e implementação de soluções sem servidor.

## <a name="big-data-processing"></a>Processamento de big data

![Mapear/reduzir diagrama](/samples/azure-samples/durablefunctions-mapreduce-dotnet/big-data-processing-serverless-mapreduce-on-azure/media/mapreducearchitecture.png)

Este exemplo usa sem servidor para fazer uma operação de mapeamento/redução em um conjunto de Big Data. Ele determina a velocidade média de viagens de táxi amarelo de Nova York por dia em 2017.

[Processamento de Big Data: MapReduce sem servidor no Azure](/samples/azure-samples/durablefunctions-mapreduce-dotnet/big-data-processing-serverless-mapreduce-on-azure/)

## <a name="create-serverless-applications-hands-on-lab"></a>Criar aplicativos sem servidor: laboratório prático

Saiba como usar as funções para executar a lógica do lado do servidor e criar arquiteturas sem servidor.

- Escolhendo o melhor serviço do Azure para sua empresa
- Criando Azure Functions
- Usando gatilhos
- Funções de encadeamento
- Fluxos de trabalho de execução longa
- Monitoramento
- Desenvolvimento, teste e implantação

[Criar aplicativos sem servidor](/learn/paths/create-serverless-applications/)

## <a name="customer-reviews"></a>Revisões do cliente

Este exemplo demonstra as novas ferramentas de Azure Functions para bibliotecas de classes C# no Visual Studio. Crie um site da Web em que os clientes enviem análises de produtos que são armazenados em blobs de armazenamento do Azure e CosmosDB. Adicione um Azure function para executar a moderação automatizada das revisões do cliente usando os serviços cognitivas do Azure. Use uma fila de armazenamento do Azure para desacoplar o site da função.

[Aplicativo de revisões de clientes com serviços cognitivas](/samples/azure-samples/functions-customer-reviews/customer-reviews-cognitive-services/)

## <a name="docker-linux-image-support"></a>Suporte a imagens do Docker para Linux

Este exemplo demonstra como criar um `Dockerfile` para compilar e executar Azure Functions em um contêiner do Docker do Linux.

[Azure Functions no Linux](/samples/azure-samples/functions-linux-custom-image/azure-functions-on-linux-custom-image-tutorial-sample-project/)

## <a name="file-processing-and-validation"></a>Processamento e validação de arquivo

Este exemplo analisa um conjunto de arquivos CSV de clientes hipotéticos. Ele garante que todos os arquivos necessários para um cliente "lote" estejam prontos e, em seguida, valida a estrutura de cada arquivo. Soluções diferentes são apresentadas usando Azure Functions, aplicativos lógicos e Durable Functions.

[Processamento e validação de arquivos usando Azure Functions, aplicativos lógicos e Durable Functions](/samples/azure-samples/serverless-file-validation/file-processing-and-validation-using-azure-functions-logic-apps-and-durable-functions/)

## <a name="game-data-visualization"></a>Visualização de dados do jogo

![Telemetria do jogo](/samples/azure-samples/gaming-in-editor-telemetry/in-editor-telemetry-visualization/media/points.png)

Um exemplo de como um desenvolvedor poderia implementar uma solução de visualização de dados no editor para seus jogos. Na verdade, um plug-in do motor 4 e um plug-in do Unity inreais foram desenvolvidos usando esse exemplo como seu back-end. O componente de serviço é independente do mecanismo de jogo.

[Visualização de telemetria do jogo no editor](/samples/azure-samples/gaming-in-editor-telemetry/in-editor-telemetry-visualization/)

## <a name="graphql"></a> GraphQL

Crie uma função sem servidor que expõe uma API GraphQL.

[Funções sem servidor para GraphQL](https://github.com/softchris/graphql-workshop-dotnet/blob/master/docs/workshop/4.md)

## <a name="internet-of-things-iot-reliable-edge-relay"></a>Retransmissão de borda confiável de Internet das Coisas (IoT)

![Arquitetura de IoT](/samples/azure-samples/iot-reliable-edge-relay/iot-reliable-edge-relay/media/architecture.png)

Este exemplo implementa um novo protocolo de comunicação para habilitar a comunicação de upstream confiável de dispositivos IoT. Ele automatiza a detecção de lacunas de dados e o aterramento.

[Retransmissão de borda confiável de IoT](/samples/azure-samples/iot-reliable-edge-relay/iot-reliable-edge-relay/)

## <a name="microservices-reference-architecture"></a>Arquitetura de referência de microserviços

![Arquitetura de referência](/samples/azure-samples/serverless-microservices-reference-architecture/serverless-microservices-reference-architecture/media/macro-architecture.png)

Uma arquitetura de referência que orienta o processo de tomada de decisão envolvido na criação, no desenvolvimento e na entrega do aplicativo Rideshare by Relecloud (uma empresa fictícia). Ele inclui instruções práticas para configurar e implantar todos os componentes da arquitetura.

[Arquitetura de referência de microserviço sem servidor](/samples/azure-samples/serverless-microservices-reference-architecture/serverless-microservices-reference-architecture/)

## <a name="migrate-console-apps-to-serverless"></a>Migrar aplicativos de console para servidor

Este exemplo é uma função genérica ( `.csx` arquivo) que pode ser usada para converter qualquer aplicativo de console em um serviço Web http no Azure functions. Tudo o que você precisa fazer é editar um arquivo de configuração e especificar quais parâmetros de entrada serão passados como argumentos para o `.exe` .

[Executar aplicativos de console no Azure Functions](/samples/azure-samples/functions-dotnet-migrating-console-apps/run-console-apps-on-azure-functions/)

## <a name="serverless-for-mobile"></a>Sem servidor para dispositivos móveis

Azure Functions são fáceis de implementar e manter e podem ser acessadas por meio de HTTP. Eles são uma ótima maneira de implementar uma API para um aplicativo móvel. A Microsoft oferece excelentes ferramentas de plataforma cruzada para iOS, Android e Windows com o Xamarin. Como tal, o Xamarin e o Azure Functions estão trabalhando muito juntos. Este artigo mostra como implementar uma função do Azure no portal do Azure ou no Visual Studio primeiro e criar um cliente de plataforma cruzada com Xamarin. Forms em execução no Android, iOS e Windows.

[Implementando uma função simples do Azure com um cliente Xamarin. Forms](/samples/azure-samples/functions-xamarin-getting-started/implementing-a-simple-azure-function-with-a-xamarinforms-client/)

## <a name="serverless-messaging"></a>Mensagens sem servidor

Este exemplo mostra como utilizar Durable Functions padrão de Fan-out para carregar um número arbitrário de mensagens em qualquer número de sessões/partições. Ele visa o barramento de serviço, hubs de eventos ou filas de armazenamento. O exemplo também adiciona a capacidade de consumir essas mensagens com outra função do Azure e carregar os dados de tempo resultantes em outro hub de eventos. Os dados são então ingeridos em serviços de análise, como o Azure Data Explorer.

[Produzir e consumir mensagens por meio do barramento de serviço, dos hubs de eventos e das filas de armazenamento com Azure Functions](/samples/azure-samples/durable-functions-producer-consumer/product-consume-messages-az-functions/)

## <a name="recommended-resources"></a>Recursos recomendados

- [Azure Functions no Linux](/samples/azure-samples/functions-linux-custom-image/azure-functions-on-linux-custom-image-tutorial-sample-project/)
- [Processamento de Big Data: MapReduce sem servidor no Azure](/samples/azure-samples/durablefunctions-mapreduce-dotnet/big-data-processing-serverless-mapreduce-on-azure/)
- [Criar aplicativos sem servidor](/learn/paths/create-serverless-applications/)
- [Aplicativo de revisões de clientes com serviços cognitivas](/samples/azure-samples/functions-customer-reviews/customer-reviews-cognitive-services/)
- [Processamento e validação de arquivos usando Azure Functions, aplicativos lógicos e Durable Functions](/samples/azure-samples/serverless-file-validation/file-processing-and-validation-using-azure-functions-logic-apps-and-durable-functions/)
- [Implementando uma função simples do Azure com um cliente Xamarin. Forms](/samples/azure-samples/functions-xamarin-getting-started/implementing-a-simple-azure-function-with-a-xamarinforms-client/)
- [Visualização de telemetria do jogo no editor](/samples/azure-samples/gaming-in-editor-telemetry/in-editor-telemetry-visualization/)
- [Retransmissão de borda confiável de IoT](/samples/azure-samples/iot-reliable-edge-relay/iot-reliable-edge-relay/)
- [Produzir e consumir mensagens por meio do barramento de serviço, dos hubs de eventos e das filas de armazenamento com Azure Functions](/samples/azure-samples/durable-functions-producer-consumer/product-consume-messages-az-functions/)
- [Executar aplicativos de console no Azure Functions](/samples/azure-samples/functions-dotnet-migrating-console-apps/run-console-apps-on-azure-functions/)
- [Funções sem servidor para GraphQL](https://github.com/softchris/graphql-workshop-dotnet/blob/master/docs/workshop/4.md)
- [Arquitetura de referência de microserviço sem servidor](/samples/azure-samples/serverless-microservices-reference-architecture/serverless-microservices-reference-architecture/)

>[!div class="step-by-step"]
>[Anterior](orchestration-patterns.md) 
> [Avançar](serverless-conclusion.md)
