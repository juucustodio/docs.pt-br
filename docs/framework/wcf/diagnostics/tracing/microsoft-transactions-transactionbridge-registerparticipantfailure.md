---
description: 'Saiba mais sobre: Microsoft. Transactions. TransactionBridge. RegisterParticipantFailure'
title: Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure
ms.date: 03/30/2017
ms.assetid: 3a4ead79-8550-4037-84e3-fd70ff56e001
ms.openlocfilehash: e930ee66720a9f397999d729e8d680fce9a37e29
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99770619"
---
# <a name="microsofttransactionstransactionbridgeregisterparticipantfailure"></a>Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure

Falha do serviço de protocolo WS-AT ao registrar um participante para um protocolo de controle.  
  
## <a name="description"></a>Descrição  

 Rastreado se o MSDTC detectar uma solicitação de registro inválida. Isso pode ser causado por várias solicitações de registro de conclusão e erros internos.  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Não tente se registrar para conclusão mais de uma vez.  Além disso, inspecione a cadeia de caracteres de status na mensagem de rastreamento para determinar se existe algum item acionável.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
