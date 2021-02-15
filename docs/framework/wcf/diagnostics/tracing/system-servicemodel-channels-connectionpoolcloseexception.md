---
description: 'Saiba mais sobre: System. ServiceModel. Channels. ConnectionPoolCloseException'
title: System.ServiceModel.Channels.ConnectionPoolCloseException
ms.date: 03/30/2017
ms.assetid: 8358898e-129e-4fac-a6bf-bf3aa4293ae2
ms.openlocfilehash: a65739cc872f3cd175d76e9113380f9f4185d498
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644626"
---
# <a name="systemservicemodelchannelsconnectionpoolcloseexception"></a>System.ServiceModel.Channels.ConnectionPoolCloseException

Ocorreu uma exceção ao fechar as conexões nesse pool de conexões.  
  
## <a name="description"></a>Descrição  

 Esse rastreamento de nível de erro indica que ocorreu um erro ao fechar os pools de conexão usados pelo recurso de pool de conexões do Windows Communication Foundation (WCF). Um motivo possível para isso é um fechamento malsucedido de uma conexão em pool ou um conjunto de conexões em pool dentro do CloseTimeout. Quando essa exceção é lançada, todas as conexões não fechadas restantes dentro desse pool são anuladas; as conexões não fechadas em outros pools são abandonadas.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
