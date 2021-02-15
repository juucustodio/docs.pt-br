---
description: 'Saiba mais sobre: mensagens suspeitas enfileiradas por segundo'
title: Mensagens suspeitas na fila por segundo
ms.date: 03/30/2017
ms.assetid: d193fdd1-02f1-44a0-906e-f632a8f574c3
ms.openlocfilehash: 3240974445debf86ff17187e4c6762b39610bd46
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99744078"
---
# <a name="queued-poison-messages-per-second"></a>Mensagens suspeitas na fila por segundo

Nome do contador: mensagens suspeitas enfileiradas por segundo.  
  
## <a name="description"></a>Descrição  

 Número de mensagens marcadas como inviabilizada pelo transporte em fila neste serviço em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
