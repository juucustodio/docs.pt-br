---
description: 'Saiba mais sobre: mensagens rejeitadas enfileiradas por segundo'
title: Mensagens em fila rejeitadas por segundo
ms.date: 03/30/2017
ms.assetid: 77ea9aa3-b9e2-4a1d-a65e-5ca115ba0567
ms.openlocfilehash: d0d227a26a49921449786d2c9f885fac13a82bde
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99744065"
---
# <a name="queued-rejected-messages-per-second"></a>Mensagens em fila rejeitadas por segundo

Nome do contador: mensagens enfileiradas rejeitadas por segundo.  
  
## <a name="description"></a>Descrição  

 Número de mensagens rejeitadas pelo transporte em fila neste serviço em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
