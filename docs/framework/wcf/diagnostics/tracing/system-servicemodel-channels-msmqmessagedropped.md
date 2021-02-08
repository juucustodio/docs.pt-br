---
description: 'Saiba mais sobre: System. ServiceModel. Channels. MsmqMessageDropped'
title: System.ServiceModel.Channels.MsmqMessageDropped
ms.date: 03/30/2017
ms.assetid: 8b6e644d-fa68-4be7-abe9-3659671a37c1
ms.openlocfilehash: 41b9c6d5399f0f6b458404ee4b64624e5863c777
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780954"
---
# <a name="systemservicemodelchannelsmsmqmessagedropped"></a>System.ServiceModel.Channels.MsmqMessageDropped

O MSMQ removeu a mensagem.  
  
## <a name="description"></a>Descrição  

 O rastreamento indica que uma mensagem MSMQ foi descartada. As mensagens MSMQ podem ser descartadas quando Windows Communication Foundation (WCF) (usado com o NetMsmqBinding ou MsmqIntegrationBinding) não puder processá-las. Essas mensagens são chamadas de mensagens suspeitas.  
  
 Uma mensagem suspeita é descartada quando a `ReceiveErrorHandling` propriedade em NetMsmqBinding ou MsmqIntegrationBinding é definida como `Drop` . Uma mensagem descartada é removida da fila e não é mais recuperável.  
  
 Para obter mais informações sobre quando as mensagens se tornam suspeitas e como configurar seu serviço para tratá-las adequadamente, consulte [manipulação de mensagens suspeitas](../../feature-details/poison-message-handling.md).  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
- [Manipulação de mensagens suspeitas](../../feature-details/poison-message-handling.md)
