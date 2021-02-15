---
description: 'Saiba mais sobre: System. ServiceModel. Channels. MsmqPoisonMessageRejected'
title: System.ServiceModel.Channels.MsmqPoisonMessageRejected
ms.date: 03/30/2017
ms.assetid: 0e64b9bd-1f12-43df-a189-d7be3c2bace1
ms.openlocfilehash: 856c28dd313867de0661d4950dd67e6740e2b338
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99759296"
---
# <a name="systemservicemodelchannelsmsmqpoisonmessagerejected"></a>System.ServiceModel.Channels.MsmqPoisonMessageRejected

Mensagem suspeita rejeitada.  
  
## <a name="description"></a>Descrição  

 O rastreamento indica que uma mensagem suspeita foi encontrada e subsequentemente rejeitada. Isso ocorre quando a `ReceiveErrorHandling` propriedade em NetMsmqBinding ou MsmqIntegrationBinding é definida como `Reject` . Uma mensagem rejeitada é entregue de volta para a [fila de mensagens mortas](../../feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)do remetente.  
  
 Para obter mais informações sobre quando as mensagens se tornam suspeitas e como configurar seu serviço para tratá-las adequadamente, consulte [manipulação de mensagens suspeitas](../../feature-details/poison-message-handling.md). Para obter mais informações sobre o que uma mensagem rejeitada significa no MSMQ, consulte [MQMarkMessageRejected](/previous-versions/windows/desktop/msmq/ms707071(v=vs.85)).  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
- [Manipulação de mensagens suspeitas](../../feature-details/poison-message-handling.md)
- [MQMarkMessageRejected](/previous-versions/windows/desktop/msmq/ms707071(v=vs.85))
