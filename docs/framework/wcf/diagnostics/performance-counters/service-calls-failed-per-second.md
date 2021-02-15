---
description: 'Saiba mais sobre: serviço: chamadas com falha por segundo'
title: 'Serviços: chamadas com falha por segundo'
ms.date: 03/30/2017
ms.assetid: 5a2c7939-107d-4f0c-b43c-e02e079e8a9d
ms.openlocfilehash: b271d5076d0f0c89c4d33b124e0184584795466a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803354"
---
# <a name="service-calls-failed-per-second"></a>Serviços: chamadas com falha por segundo

Nome do contador: chamadas com falha por segundo.  
  
## <a name="description"></a>Descrição  

 Número de chamadas que têm exceções sem tratamento e são recebidas por esse serviço em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)  
  
 No código gerenciado, as exceções são geradas quando ocorrem condições de erro.  
  
 No código gerenciado, as exceções são geradas quando ocorrem condições de erro.  
  
 Esse contador é incrementado toda vez que há uma exceção sem tratamento nesse serviço.  
  
## <a name="see-also"></a>Consulte também

- [Especificando e lidando com falhas em contratos e serviços](../../specifying-and-handling-faults-in-contracts-and-services.md)
