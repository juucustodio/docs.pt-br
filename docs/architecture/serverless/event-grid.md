---
title: Grade de eventos do Azure-aplicativos sem servidor
description: A grade de eventos do Azure é uma solução sem servidor para entrega e roteamento de eventos confiáveis em grande escala em um modelo de pagamento por evento.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 04/06/2020
ms.openlocfilehash: 30937bafd8069eb4508dce18351964103421373a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171878"
---
# <a name="event-grid"></a>Grade de Eventos

A [grade de eventos do Azure](/azure/event-grid/overview) fornece a infraestrutura sem servidor para aplicativos baseados em eventos. Você pode publicar na grade de eventos de qualquer fonte e consumir mensagens de qualquer plataforma. A grade de eventos também tem suporte interno para eventos de recursos do Azure para simplificar a integração com seus aplicativos. Por exemplo, você pode assinar eventos de armazenamento de BLOBs para notificar seu aplicativo quando um arquivo for carregado. Em seguida, seu aplicativo pode publicar uma mensagem de grade de eventos personalizada consumida por outros aplicativos na nuvem ou locais. A grade de eventos foi criada para lidar de forma confiável em grande escala. Você Obtém os benefícios de publicar e assinar mensagens sem a sobrecarga de configurar a infraestrutura necessária.

![Logotipo da grade de eventos](./media/event-grid-logo.png)

Os principais recursos da grade de eventos incluem:

- Roteamento de eventos totalmente gerenciado.
- Entrega de eventos quase em tempo real em escala.
- Cobertura ampla dentro e fora do Azure.

## <a name="scenarios"></a>Cenários

A grade de eventos aborda vários cenários diferentes. Esta seção aborda três dos mais comuns.

### <a name="ops-automation"></a>Automação de operações

![Automação de operações](./media/ops-automation.png)

A grade de eventos pode ajudar a acelerar a automação e simplificar a imposição de políticas notificando a [automação do Azure](/azure/automation) quando a infraestrutura é provisionada.

### <a name="application-integration"></a>Integração de aplicativos

![Integração de aplicativos](./media/app-integration.png)

Você pode usar a grade de eventos para conectar seu aplicativo a outros serviços. Usando protocolos HTTP padrão, até mesmo aplicativos herdados podem ser facilmente modificados para publicar mensagens de grade de eventos. Os ganchos da Web estão disponíveis para outros serviços e plataformas para consumir mensagens da grade de eventos.

### <a name="serverless-apps"></a>Aplicativos sem servidor

![Aplicativos sem servidor](./media/serverless-apps.png)

A grade de eventos pode disparar Azure Functions, aplicativos lógicos ou seu próprio código personalizado. Uma grande vantagem de usar a grade de eventos é que ela usa um mecanismo de *Push* para enviar mensagens quando ocorrem eventos. A arquitetura de push consome menos recursos e dimensiona melhor do que os mecanismos de *sondagem* . A sondagem deve verificar se há atualizações em um intervalo regular.

## <a name="event-grid-vs-other-azure-messaging-services"></a>Grade de eventos versus outros serviços de mensagens do Azure

O Azure fornece vários serviços de mensagens, incluindo [hubs de eventos](/azure/event-hubs) e [barramento de serviço](/azure/service-bus-messaging). Cada um foi projetado para atender a um conjunto específico de casos de uso. O diagrama a seguir fornece uma visão geral de alto nível das diferenças entre os serviços.

![Comparação de mensagens do Azure](./media/azure-messaging-services.png)

Para obter uma comparação mais detalhada, consulte [comparar serviços de mensagens](/azure/event-grid/compare-messaging-services).

## <a name="performance-targets"></a>Destinos de desempenho

Usando a grade de eventos, você pode aproveitar as seguintes garantias de desempenho:

- Latência de ponta a ponta de subsegundos no 99 º percentil.
- disponibilidade de 99,99%.
- 10 milhões eventos por segundo por região.
- 100 milhões assinaturas por região.
- 50-latência do Publicador MS.
- repetição de 24 horas com retirada exponencial para entrega garantida na janela de um dia.
- Failover regional transparente.

## <a name="event-grid-schema"></a>Esquema da Grade de Eventos

A grade de eventos usa um esquema padrão para encapsular eventos personalizados. O esquema é como um envelope que encapsula o elemento de dados personalizado. Aqui está um exemplo de mensagem de grade de eventos:

```json
[{
    "id": "03e24f21-a955-43cc-8921-1f61a6081ce0",
    "eventType": "myCustomEvent",
    "subject": "foo/bar/12",
    "eventTime": "2018-09-22T10:36:01+00:00",
    "data": {
        "favoriteColor": "blue",
        "favoriteAnimal": "panther",
        "favoritePlanet": "Jupiter"
    },
    "dataVersion": "1.0"
}]
```

Tudo sobre a mensagem é padrão, exceto a `data` propriedade. Você pode inspecionar a mensagem e usar `eventType` e `dataVersion` para desserializar a parte personalizada da carga.

## <a name="azure-resources"></a>Recursos do Azure

Uma grande vantagem de usar a grade de eventos são as mensagens automáticas produzidas pelo Azure. No Azure, os recursos são publicados automaticamente em um *tópico* que permite que você assine vários eventos. A tabela a seguir lista os tipos de recursos, tipos de mensagem e eventos que estão disponíveis automaticamente.

| Recursos do Azure | Tipo de evento | Descrição |
| -------------- | ---------- | ----------- |
| Assinatura do Azure | Microsoft.Resources.ResourceWriteSuccess | Gerado quando um recurso cria ou operação de atualização será bem-sucedida. |
| | Microsoft.Resources.ResourceWriteFailure | Gerado quando um recurso cria ou operação de atualização será falha. |
| | Microsoft.Resources.ResourceWriteCancel | Gerado quando um recurso cria ou operação de atualização é cancelada. |
|  | Microsoft.Resources.ResourceDeleteSuccess | Gerado quando um recurso cria ou operação de atualização é bem-sucedida. |
|  | Microsoft.Resources.ResourceDeleteFailure | Gerado quando um recurso cria ou operação de atualização é falha. |
| | Microsoft.Resources.ResourceDeleteCancel | Gerado quando um recurso cria ou operação de atualização é cancelada. Esse evento ocorre quando a implantação de um modelo é cancelada. |
| Armazenamento de Blobs | Microsoft.Storage.BlobCreated | Gerado quando um blob é criado. |
| | Microsoft.Storage.BlobDeleted | Gerado quando um blob é deletado. |
| Hubs de Eventos | Microsoft. EventHub. CaptureFileCreated | Gerado quando um arquivo de captura é criado.
| Hub IoT | Microsoft.Devices.DeviceCreated | Publicado quando um dispositivo é registrado para um Hub IoT. |
| | Microsoft.Devices.DeviceDeleted | Publicado quando um dispositivo é excluído de um Hub IoT. |
| Grupos de recursos | Microsoft.Resources.ResourceWriteSuccess | Gerado quando um recurso cria ou operação de atualização será bem-sucedida. |
| | Microsoft.Resources.ResourceWriteFailure | Gerado quando um recurso cria ou operação de atualização será falha. |
| | Microsoft.Resources.ResourceWriteCancel | Gerado quando um recurso cria ou operação de atualização é cancelada. |
| | Microsoft.Resources.ResourceDeleteSuccess | Gerado quando um recurso cria ou operação de atualização é bem-sucedida. |
| | Microsoft.Resources.ResourceDeleteFailure | Gerado quando um recurso cria ou operação de atualização é falha. |
| | Microsoft.Resources.ResourceDeleteCancel | Gerado quando um recurso cria ou operação de atualização é cancelada. Esse evento ocorre quando a implantação de um modelo é cancelada. |

Para obter mais informações, consulte [esquema de eventos da grade de eventos do Azure](/azure/event-grid/event-schema).

Você pode acessar a grade de eventos de qualquer tipo de aplicativo, mesmo um que seja executado localmente.

## <a name="conclusion"></a>Conclusão

Neste capítulo, você aprendeu sobre a plataforma sem servidor do Azure que é composta de Azure Functions, aplicativos lógicos e grade de eventos. Você pode usar esses recursos para criar uma arquitetura de aplicativo totalmente sem servidor ou criar uma solução híbrida que interaja com outros recursos de nuvem e servidores locais. Combinado com uma plataforma de dados sem servidor, como o [Azure SQL](/azure/sql-database) ou o [CosmosDB](/azure/cosmos-db/introduction), você pode criar aplicativos nativos de nuvem totalmente gerenciados.

## <a name="recommended-resources"></a>Recursos recomendados

- [Planos do serviço de aplicativo](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)
- [Application Insights](/azure/application-insights)
- [Análise do Application Insights](/azure/application-insights/app-insights-analytics)
- [Azure: Traga seu aplicativo para a nuvem com Azure Functions sem servidor](https://channel9.msdn.com/events/Connect/2017/E102)
- [Grade de Eventos do Azure](/azure/event-grid/overview)
- [Esquema de eventos da Grade de Eventos do Azure](/azure/event-grid/event-schema)
- [Hubs de eventos do Azure](/azure/event-hubs)
- [Documentação do Azure Functions](/azure/azure-functions)
- [Conceitos de gatilhos e de associações do Azure Functions](/azure/azure-functions/functions-triggers-bindings)
- [Aplicativos Lógicos do Azure](/azure/logic-apps)
- [Barramento de Serviço do Azure](/azure/service-bus-messaging)
- [Armazenamento de Tabelas do Azure](/azure/cosmos-db/table-storage-overview)
- [Conectar-se a fontes de dados locais com o Gateway de Dados Local do Azure](/azure/analysis-services/analysis-services-gateway)
- [Criar sua primeira função no portal do Azure](/azure/azure-functions/functions-create-first-azure-function)
- [Criar sua primeira função usando a CLI do Azure](/azure/azure-functions/functions-create-first-azure-function-azure-cli)
- [Criar sua primeira função usando o Visual Studio](/azure/azure-functions/functions-create-your-first-function-visual-studio)
- [Idiomas com suporte de funções](/azure/azure-functions/supported-languages)
- [Monitorar Azure Functions](/azure/azure-functions/functions-monitoring)

>[!div class="step-by-step"]
>[Anterior](logic-apps.md) 
> [Avançar](durable-azure-functions.md)
