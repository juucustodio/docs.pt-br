---
description: 'Saiba mais sobre: sessões de mensagens confiáveis com falha por segundo'
title: Sessões de transmissão de mensagens confiáveis com falha por segundo
ms.date: 03/30/2017
ms.assetid: 8f8ca2eb-1be4-4b6a-aa78-fcd3ee145fe8
ms.openlocfilehash: 11759ad659d9e860c94b4428091fc0852ebf038c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716283"
---
# <a name="reliable-messaging-sessions-faulted-per-second"></a>Sessões de transmissão de mensagens confiáveis com falha por segundo

Nome do contador: sessões de mensagens confiáveis com falha por segundo.  
  
## <a name="description"></a>Descrição  

 Número de sessões de mensagens confiáveis com falha neste serviço em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
