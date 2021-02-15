---
description: 'Saiba mais sobre: ponto de extremidade: chamadas por segundo'
title: 'Ponto de extremidade: chamadas por segundo'
ms.date: 03/30/2017
ms.assetid: ca0fc06d-d68f-4236-bd5f-c7ff6214acdd
ms.openlocfilehash: 10e3cb892119999225abaa8b85ea59065650795d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99759569"
---
# <a name="endpoint-calls-per-second"></a>Ponto de extremidade: chamadas por segundo

Nome do contador: chamadas por segundo.  
  
## <a name="description"></a>Descrição  

 Número de chamadas para esse ponto de extremidade em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
