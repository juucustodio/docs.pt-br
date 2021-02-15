---
description: 'Saiba mais sobre: mensagens de mensagens confiáveis eliminadas por segundo'
title: Mensagens Confiáveis Ignoradas por Segundo
ms.date: 03/30/2017
ms.assetid: a11b0b80-b242-48e1-b0bb-7f756db5486b
ms.openlocfilehash: 6132316f100cecdba357a6da071e23de8c9a2181
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99655104"
---
# <a name="reliable-messaging-messages-dropped-per-second"></a>Mensagens Confiáveis Ignoradas por Segundo

Nome do contador: sessões de mensagens confiáveis eliminadas por segundo.  
  
## <a name="description"></a>Descrição  

 Número total de mensagens de mensagens confiáveis que foram descartadas neste serviço em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
