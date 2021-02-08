---
description: 'Saiba mais sobre: System. ServiceModel. Channels. PeerFlooderReceiveMessageQuotaExceeded'
title: System.ServiceModel.Channels.PeerFlooderReceiveMessageQuotaExceeded
ms.date: 03/30/2017
ms.assetid: b8371d0a-843e-440b-b86a-6996db131cb0
ms.openlocfilehash: 8ad164b253491f3a533c4828cd76f915eb5aed68
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780863"
---
# <a name="systemservicemodelchannelspeerflooderreceivemessagequotaexceeded"></a>System.ServiceModel.Channels.PeerFlooderReceiveMessageQuotaExceeded

A taxa de recebimento de mensagens de entrada é muito alta.  
  
## <a name="description"></a>Descrição  

 Esse rastreamento ocorre ao tentar processar mensagens de entrada. Uma mensagem não pôde ser encaminhada para um vizinho específico porque o conjunto de cotas para esse vizinho foi excedido. Isso ocorre quando um vizinho sem resposta falha ao limpar uma pendência de mensagens pendentes para esse vizinho.  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Reduza a taxa em que as mensagens são enviadas dentro da malha.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
