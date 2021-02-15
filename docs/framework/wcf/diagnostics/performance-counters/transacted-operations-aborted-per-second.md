---
description: 'Saiba mais sobre: operações transacionadas anuladas por segundo'
title: Operações Transacionadas Anuladas por Segundo
ms.date: 03/30/2017
ms.assetid: 19fc993f-2b3d-4898-852e-3b98ec2153a5
ms.openlocfilehash: de130c18e065e48ed7ac18442b2bc5f82c2f6861
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99771191"
---
# <a name="transacted-operations-aborted-per-second"></a>Operações Transacionadas Anuladas por Segundo

Nome do contador: operações transacionadas anuladas por segundo.  
  
## <a name="description"></a>Descrição  

 Número de operações transacionais que foram anuladas neste serviço em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
