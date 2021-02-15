---
description: 'Saiba mais sobre: System. ServiceModel. Channels. MsmqMoveOrDeleteAttemptFailed'
title: System.ServiceModel.Channels.MsmqMoveOrDeleteAttemptFailed
ms.date: 03/30/2017
ms.assetid: d75d39da-7502-4a6a-91b9-eaa05b8e24d5
ms.openlocfilehash: 7b3c8dad9e3a3e88dff72706917f3729d55b3799
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99769735"
---
# <a name="systemservicemodelchannelsmsmqmoveordeleteattemptfailed"></a>System.ServiceModel.Channels.MsmqMoveOrDeleteAttemptFailed

Não é possível mover ou excluir a mensagem.  
  
## <a name="description"></a>Descrição  

 O rastreamento indica que uma falha ocorreu ao tentar mover, excluir ou rejeitar uma mensagem MSMQ.  
  
 As mensagens MSMQ são empregadas por Windows Communication Foundation (WCF) (quando usadas com NetMsmqBinding ou MsmqIntegrationBinding). Esse rastreamento está relacionado ao valor escolhido da `ReceiveErrorHandling` propriedade em NetMsmqBinding ou MsmqIntegrationBinding.  
  
 Esse rastreamento não indica uma falha geral do sistema. No entanto, isso indica que a disposição de mensagem suspeita escolhida falhou para uma mensagem. Para obter mais informações sobre quando as mensagens se tornam suspeitas e como configurar seu serviço para tratá-las adequadamente, consulte [manipulação de mensagens suspeitas](../../feature-details/poison-message-handling.md).  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
