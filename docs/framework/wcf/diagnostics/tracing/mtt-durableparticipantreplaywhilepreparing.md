---
description: 'Saiba mais sobre: Microsoft. Transactions. TransactionBridge. DurableParticipantReplayWhilePreparing'
title: Microsoft.Transactions.TransactionBridge.DurableParticipantReplayWhilePreparing
ms.date: 03/30/2017
ms.assetid: 10ef3876-6f8e-4d4e-8444-f47847b64795
ms.openlocfilehash: fcaa50dd4faa548cad8ff085f1c66f94c63bd010
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99635656"
---
# <a name="microsofttransactionstransactionbridgedurableparticipantreplaywhilepreparing"></a>Microsoft.Transactions.TransactionBridge.DurableParticipantReplayWhilePreparing

O serviço de protocolo WS-AT recebeu uma mensagem de reprodução de um participante durável, que não respondeu à preparação. Consequentemente, a transação foi anulada.  
  
## <a name="description"></a>Descrição  

 Rastreado se uma mensagem de reprodução for recebida enquanto um participante durável ainda estiver se preparando. Esta é uma mensagem ilegal para esse Estado e a transação será anulada.  
  
## <a name="troubleshooting"></a>Solução de problemas

Receber esse erro pode indicar que um participante durável (incluindo TransactionManagers subordinados) se recuperou de uma falha; no entanto, não há certeza do resultado da transação e solicita seu status.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
