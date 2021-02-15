---
description: 'Saiba mais sobre: System. ServiceModel. Channels. MsmqMessageRejected'
title: System.ServiceModel.Channels.MsmqMessageRejected
ms.date: 03/30/2017
ms.assetid: 9b7c10a7-2af6-44a2-8b1a-90bba0c7cf26
ms.openlocfilehash: 4400519c814627fd2a2f2585359d6d6376798ac0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780941"
---
# <a name="systemservicemodelchannelsmsmqmessagerejected"></a>System.ServiceModel.Channels.MsmqMessageRejected

O MSMQ rejeitou a mensagem.  
  
## <a name="description"></a>Descrição  

 Esse rastreamento indica que uma mensagem MSMQ foi rejeitada.  
  
 As mensagens MSMQ podem ser rejeitadas quando Windows Communication Foundation (WCF) (usado com o NetMsmqBinding ou MsmqIntegrationBinding) não puder processá-las. Essas mensagens são chamadas de mensagens suspeitas. Uma mensagem suspeita é rejeitada quando a `ReceiveErrorHandling` propriedade em NetMsmqBinding ou MsmqIntegrationBinding é definida como `Reject` . Uma mensagem rejeitada é entregue de volta para a [fila de mensagens mortas](../../feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)do remetente.  
  
 Para obter mais informações sobre quando as mensagens se tornam suspeitas e como configurar seu serviço para tratá-las adequadamente, consulte [manipulação de mensagens suspeitas](../../feature-details/poison-message-handling.md).  
  
 Para obter mais informações sobre o que uma mensagem rejeitada significa no MSMQ, consulte [MQMarkMessageRejected](/previous-versions/windows/desktop/msmq/ms707071(v=vs.85)).  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
- [Manipulação de mensagens suspeitas](../../feature-details/poison-message-handling.md)
- [MQMarkMessageRejected](/previous-versions/windows/desktop/msmq/ms707071(v=vs.85))
