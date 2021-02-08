---
description: 'Saiba mais sobre: Microsoft. Transactions. TransactionBridge. ReplayMessageRetry'
title: Microsoft.Transactions.TransactionBridge.ReplayMessageRetry
ms.date: 03/30/2017
ms.assetid: e5b820ae-504d-405a-926a-9effa41d2369
ms.openlocfilehash: e4de1416fab2cf7098d0276b6130999c01ea6e3e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803250"
---
# <a name="microsofttransactionstransactionbridgereplaymessageretry"></a>Microsoft.Transactions.TransactionBridge.ReplayMessageRetry

Uma nova tentativa de mensagem de reprodução foi enviada a um coordenador sem resposta.  
  
## <a name="description"></a>Descrição  

 Rastreado se o Gerenciador de transações local precisar reenviar uma mensagem de reprodução para um coordenador superior porque ele não recebeu uma resposta em um determinado período de tempo.  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Investigue possíveis problemas de rede ou de produtos que impedem que a resposta seja entregue no prazo.  Se muitas dessas mensagens forem vistas, isso poderá indicar problemas de infraestrutura ou tempos de resposta muito longos. Os dois problemas reduzem drasticamente a taxa de transferência das transações no sistema.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
