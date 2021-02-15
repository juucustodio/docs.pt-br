---
description: 'Saiba mais sobre: System. ServiceModel. TxCompletionStatusAbortedOnSessionClose'
title: System.ServiceModel.TxCompletionStatusAbortedOnSessionClose
ms.date: 03/30/2017
ms.assetid: 7e142e9d-e81b-4309-974a-02e9cc064ea0
ms.openlocfilehash: d47dc1a87c7f44b58f70f9590b4233f1e0a9074e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735706"
---
# <a name="systemservicemodeltxcompletionstatusabortedonsessionclose"></a>System.ServiceModel.TxCompletionStatusAbortedOnSessionClose

A transação especificada foi anulada porque estava incompleta quando a sessão foi fechada e o TransactionAutoCompleteOnSessionClose OperationBehaviorAttribute foi definido como falso.  
  
## <a name="description"></a>Descrição  

 Rastreado se a sessão ativa atual foi fechada e a transação não foi concluída e a TransactionAutoCompleteOnSessionClose está definida como `false` .  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Esse rastreamento indica um possível bug de aplicativo que deve ser investigado.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
