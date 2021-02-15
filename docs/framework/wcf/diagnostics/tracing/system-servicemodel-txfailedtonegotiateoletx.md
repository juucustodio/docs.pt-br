---
description: 'Saiba mais sobre: System. ServiceModel. TxFailedToNegotiateOleTx'
title: System.ServiceModel.TxFailedToNegotiateOleTx
ms.date: 03/30/2017
ms.assetid: 3f0f0b4b-a1ad-4704-8329-455daf54892d
ms.openlocfilehash: c7f18ef73ff9c09cc51ad3aa6c54c2bd672d0cc3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735563"
---
# <a name="systemservicemodeltxfailedtonegotiateoletx"></a>System.ServiceModel.TxFailedToNegotiateOleTx

A negociação do protocolo OleTransactions não pôde ser concluída para o contexto de coordenação especificado.  
  
## <a name="description"></a>Descrição  

 Rastreado quando uma transação de entrada com informações de OleTx não é capaz de usar as informações de OleTx anexadas e voltará a usar WS-AT em vez disso.  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Indica um possível problema com a comunicação de RPC do MSDTC entre os computadores. Se muitos desses rastreamentos aparecerem no log, uma diminuição drástica no desempenho poderá resultar.  Se OleTx não for desejado, defina `OleTxUpgradeEnabled` como 0 na configuração do registro WS-AT.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
