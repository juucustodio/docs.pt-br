---
description: 'Saiba mais sobre: Microsoft. Transactions. TransactionBridge. VolatileOutcomeTimeout'
title: Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout
ms.date: 03/30/2017
ms.assetid: 2dbe34c5-57c7-4b64-9257-63021911d03c
ms.openlocfilehash: 5dd6ecce995d315581e1335e4dc83c425a6381b7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99677230"
---
# <a name="microsofttransactionstransactionbridgevolatileoutcometimeout"></a>Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout

O tempo limite do serviço de protocolo WS-AT expirou ao aguardar uma resposta a uma mensagem de resultado de um participante volátil. O resultado da transação pode estar em dúvida se o participante retornar.  
  
## <a name="description"></a>Descrição  

 Rastreado quando um participante volátil decidiu confirmar ou anular, mas não respondeu a uma solicitação de confirmação ou reversão em um determinado período de tempo.  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Certifique-se de que todos os participantes voláteis sejam capazes de responder dentro do período determinado. O período de tempo padrão é de 180 segundos.  Se isso for insuficiente, aumente a `VolatileOutcomeDelay` política de temporizador para WS-AT.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
