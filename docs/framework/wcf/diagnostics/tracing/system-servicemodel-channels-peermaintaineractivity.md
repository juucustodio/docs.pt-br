---
description: 'Saiba mais sobre: System. ServiceModel. Channels. PeerMaintainerActivity'
title: System.ServiceModel.Channels.PeerMaintainerActivity
ms.date: 03/30/2017
ms.assetid: ef28d086-d7fb-4e81-82e9-45a54647783b
ms.openlocfilehash: da4e4cf87da808cb6779445b6507b51d098132b3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780871"
---
# <a name="systemservicemodelchannelspeermaintaineractivity"></a>System.ServiceModel.Channels.PeerMaintainerActivity

O módulo PeerMaintainer está executando uma operação específica (detalhes contidos no corpo da mensagem de rastreamento).  
  
## <a name="description"></a>Descrição  

 Esse rastreamento ocorre durante várias operações de PeerMaintainer.  
  
 PeerMaintainer é um componente interno do PeerNode. A cada minuto, ou a cada 32 mensagens recebidas, ele envia uma mensagem LinkUtility para seus vizinhos com estatísticas sobre quantas mensagens são trocadas e quantos são úteis (não duplicados, não violados). Isso ajuda a determinar o utilitário de link de um vizinho específico. Aproximadamente a cada cinco minutos, o mantenedor verifica a integridade das conexões vizinhas. Se o número de conexões vizinhas exceder o valor ideal, o mantenedor removerá as conexões menos úteis. Se não houver conexões suficientes, o mantenedor adquirirá novas conexões.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
