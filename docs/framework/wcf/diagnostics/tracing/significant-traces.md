---
description: 'Saiba mais sobre: rastreamentos significativos'
title: Rastreamentos significativos
ms.date: 03/30/2017
ms.assetid: 40a1770e-3b09-4142-b0dd-f9ef73642074
ms.openlocfilehash: 6d3e12c82312c2a8a3f0a19b4dc50e99e21b9730
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99635539"
---
# <a name="significant-traces"></a>Rastreamentos significativos

Este tópico lista alguns dos principais rastreamentos emitidos por Windows Communication Foundation (WCF).  
  
## <a name="significant-traces"></a>Rastreamentos significativos  
  
|Trace|Descrição|  
|-----------|-----------------|  
|Rastreamento do log de mensagens|O rastreamento é emitido quando uma mensagem do WCF é registrada pelo recurso de log de mensagens quando a `System.ServiceModel.MessageLogging` origem do rastreamento está habilitada. Clicar nesse rastreamento exibe a mensagem. Há quatro pontos de registro em log configuráveis para uma mensagem: `ServiceLevelSendRequest` , `TransportSend` ,, `TransportReceive` `ServiceLevelReceiveRequest` , também indicada pelo atributo origem da mensagem no rastreamento do log de mensagens.|  
|Rastreamento de mensagem recebida|Esse rastreamento é emitido quando uma mensagem do WCF é recebida se a `System.ServiceModel` origem do rastreamento está habilitada no nível de informações ou detalhado. Esse rastreamento é necessário para ver a seta de correlação de mensagem na exibição de gráfico de atividade.|  
|Rastreamento de mensagem enviada|Esse rastreamento é emitido quando uma mensagem do WCF é enviada se a `System.ServiceModel` origem do rastreamento está habilitada no nível de informações ou detalhado. Esse rastreamento é necessário para ver a seta de correlação de mensagem na exibição de gráfico de atividade.|  
|Obter ChannelEndpointElement|Esse rastreamento é emitido na construção de fábrica de canal, no nível de informação. Ele fornece uma descrição do ponto de extremidade ao qual o cliente está se comunicando (endereço remoto, associação, nome do contrato).|  
|Obter ServiceElement|Esse rastreamento é emitido no host do serviço de construção, no nível de informações. Ele fornece uma descrição do contrato de serviço e da associação.|  
|SocketConnection criar|Esse rastreamento é emitido na primeira ação de processo executada pelo cliente e na atividade receber bytes no serviço. Ele fornece os endereços IP locais e remotos. Ele é emitido no nível de informação.|
