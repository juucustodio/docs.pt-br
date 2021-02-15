---
description: 'Saiba mais sobre: agendando threads'
title: Agendando threads
ms.date: 03/30/2017
helpviewer_keywords:
- threading [.NET], scheduling
- scheduling threads
ms.assetid: 67e4a0eb-3095-4ea7-b20f-908faa476277
ms.openlocfilehash: 61627a5b669e946116eaec03dbd93ab34bbfea9a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792356"
---
# <a name="scheduling-threads"></a>Agendando threads

Cada thread tem uma prioridade atribuída. Os threads criados dentro do Common Language Runtime recebem inicialmente a prioridade <xref:System.Threading.ThreadPriority.Normal?displayProperty=nameWithType>. Threads criados fora do Runtime retêm a prioridade que tinham antes de entrarem no ambiente gerenciado. Você pode obter ou definir a prioridade de qualquer thread com a propriedade <xref:System.Threading.Thread.Priority?displayProperty=nameWithType>.  
  
 Threads são agendados para execução com base em sua prioridade. Mesmo que os threads sejam executados no Runtime, todos são atribuídos frações de tempo do processador pelo sistema operacional. Os detalhes do algoritmo de agendamento usado para determinar a ordem na qual os threads são executados variam de acordo com cada sistema operacional. Em alguns sistemas operacionais, o thread com a prioridade mais alta (dos threads que podem ser executados) sempre é programada para ser executado primeiro. Se vários threads com a mesma prioridade estiverem disponíveis, o agendador percorre os threads com essa prioridade, fornecendo uma fração de tempo fixa na qual executar cada thread. Enquanto houver um thread com uma prioridade mais alta estiver disponível para execução, threads com prioridades inferiores não serão executados. Quando não houver mais nenhum threads executável com determinada prioridade, o agendador passará para a próxima prioridade mais alta e agendará a execução dos threads com essa prioridade. Se um thread de prioridade mais alta se tornar executável, o thread de prioridade mais baixo será ignorado e o thread de prioridade mais alta poderá ser executado novamente. Além disso, o sistema operacional também poderá ajustar as prioridades de threads dinamicamente conforme a interface de usuário do aplicativo é movida entre o primeiro e segundo plano. Outros sistemas operacionais podem optar por usar um algoritmo de programação diferente.  
  
## <a name="see-also"></a>Consulte também

- [Usando threads e threading](using-threads-and-threading.md)
- [Threading gerenciado e não gerenciado no Windows](managed-and-unmanaged-threading-in-windows.md)
