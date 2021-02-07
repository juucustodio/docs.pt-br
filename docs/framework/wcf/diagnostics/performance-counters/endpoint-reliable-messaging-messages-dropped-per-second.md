---
description: 'Saiba mais sobre: ponto de extremidade: mensagens de mensagens confiáveis eliminadas por segundo'
title: 'Ponto de extremidade: mensagens confiáveis do sistema de mensagens descartadas por segundo'
ms.date: 03/30/2017
ms.assetid: ea3c4fc0-1e0f-4863-8879-57bc6c113018
ms.openlocfilehash: 257ea74aeb23ef8962ce8910dee635b83f76d960
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735875"
---
# <a name="endpoint-reliable-messaging-messages-dropped-per-second"></a>Ponto de extremidade: mensagens confiáveis do sistema de mensagens descartadas por segundo

Nome do contador: sessões de mensagens confiáveis eliminadas por segundo.  
  
## <a name="description"></a>Descrição  

 Número total de mensagens de mensagens confiáveis que foram descartadas neste ponto de extremidade em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
