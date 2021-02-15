---
description: 'Saiba mais sobre: transações fluidas por segundo'
title: Fluxo de transações por segundo
ms.date: 03/30/2017
ms.assetid: b9f661e1-576c-48fc-9fdf-91853e0749e8
ms.openlocfilehash: f37c79e89efb8a013719f44350772919b7222a61
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99770996"
---
# <a name="transactions-flowed-per-second"></a>Fluxo de transações por segundo

Nome do contador: transações fluidas por segundo  
  
## <a name="description"></a>Descrição  

 Número de transações fluidas para esta operação em um segundo. Esse contador é incrementado sempre que uma ID de transação está presente em uma mensagem que é enviada para a operação.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
