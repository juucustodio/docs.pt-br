---
description: 'Saiba mais sobre: ponto de extremidade: chamadas com falha por segundo'
title: 'Ponto de extremidade: chamadas com falha por segundo'
ms.date: 03/30/2017
ms.assetid: bcbe9da4-c8dd-4e27-b630-11611adc7580
ms.openlocfilehash: 262f0fdf0750e8fdb179d41d1a99788784270023
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99759634"
---
# <a name="endpoint-calls-failed-per-second"></a>Ponto de extremidade: chamadas com falha por segundo

Nome do contador: chamadas com falha por segundo.  
  
## <a name="description"></a>Descrição  

 Número de chamadas que têm exceções sem tratamento e são recebidas por esse ponto de extremidade em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)  
  
 Esse contador é incrementado toda vez que há uma exceção sem tratamento neste ponto de extremidade.  
  
## <a name="see-also"></a>Consulte também

- [Especificando e lidando com falhas em contratos e serviços](../../specifying-and-handling-faults-in-contracts-and-services.md)
