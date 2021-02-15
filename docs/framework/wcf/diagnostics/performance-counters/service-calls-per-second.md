---
description: 'Saiba mais sobre: serviço: chamadas por segundo'
title: 'Serviço: chamadas por segundo'
ms.date: 03/30/2017
ms.assetid: 6261d28d-d449-425a-b9fc-a4ee14079134
ms.openlocfilehash: f6e21f5f1c7a0d5d4ceeb11f954ebbc95f66a3ac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99744026"
---
# <a name="service-calls-per-second"></a>Serviço: chamadas por segundo

Nome do contador: chamadas por segundo.  
  
## <a name="description"></a>Descrição  

 Número de chamadas para esse serviço em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F) em que o numerador (N) representa o número de operações executadas durante o último intervalo de amostragem, o denominador (D) representa o número de tiques decorridos durante o último intervalo de amostragem e F é a frequência das tiques.
