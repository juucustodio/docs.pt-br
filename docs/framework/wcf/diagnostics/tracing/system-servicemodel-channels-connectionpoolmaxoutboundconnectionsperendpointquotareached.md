---
description: 'Saiba mais sobre: Microsoft. Transactions. TransactionBridge. EnlistTransactionFailure'
title: Microsoft.Transactions.TransactionBridge.EnlistTransactionFailure
ms.date: 03/30/2017
ms.assetid: 1b9f5139-e122-4716-9ef7-2f38e1813993
ms.openlocfilehash: f0645d0f7bfc2787f4bce254ea8d6e3143dc0406
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644600"
---
# <a name="microsofttransactionstransactionbridgeenlisttransactionfailure"></a>Microsoft.Transactions.TransactionBridge.EnlistTransactionFailure

Falha do serviço de protocolo WS-AT ao inscrever-se em uma transação usando o contexto de coordenação fornecido.  
  
## <a name="description"></a>Descrição  

 Rastreado quando o MSDTC não pode se inscrever em uma transação para um determinado protocolo 2PC.  Isso pode acontecer porque a transação não existe mais, a lista de inlistagem não é mais permitida ou muitas inlistagens já estão presentes.  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Inspecione a cadeia de caracteres de status na mensagem de rastreamento para determinar se existe algum item acionável.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
