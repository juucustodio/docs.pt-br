---
description: 'Saiba mais sobre: Microsoft. Transactions. TransactionBridge. PreparedMessageRetry'
title: Microsoft.Transactions.TransactionBridge.PreparedMessageRetry
ms.date: 03/30/2017
ms.assetid: 2194292d-bf5f-4aef-9336-cd3c4795cb71
ms.openlocfilehash: 99106493f0eec900875a713b439111fadb150c62
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99677269"
---
# <a name="microsofttransactionstransactionbridgepreparedmessageretry"></a>Microsoft.Transactions.TransactionBridge.PreparedMessageRetry

Uma nova tentativa de mensagem preparada foi enviada a um coordenador sem resposta.  
  
## <a name="description"></a>Descrição  

 Rastreado se o Gerenciador de transações local precisar reenviar uma mensagem preparada para um coordenador superior porque ele não recebeu uma resposta em um determinado período/  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Investigue possíveis problemas de rede ou de produtos que impedem que a resposta seja entregue no prazo.  Se muitas dessas mensagens forem vistas, isso poderá indicar problemas de infraestrutura ou tempos de resposta muito longos. Os dois problemas reduzem drasticamente a taxa de transferência das transações no sistema.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
