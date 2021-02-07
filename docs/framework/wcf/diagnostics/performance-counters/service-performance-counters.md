---
description: 'Saiba mais sobre: contadores de desempenho de serviço'
title: Contadores de desempenho de serviço
ms.date: 03/30/2017
ms.assetid: 4210f549-31f2-4ea7-99bd-69eaffb98ddf
ms.openlocfilehash: 16f6f2548cf7f92b64264ac606423c69e62cd110
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686031"
---
# <a name="service-performance-counters"></a>Contadores de desempenho de serviço

Os contadores de desempenho de serviço medem o comportamento do serviço como um todo e podem ser usados para diagnosticar o desempenho do serviço inteiro. Eles podem ser encontrados no `ServiceModelService 4.0.0.0` objeto de desempenho ao exibir com o monitor de desempenho (Perfmon.exe). As instâncias são nomeadas usando o seguinte padrão:  
  
`ServiceName@ServiceBaseAddress`
  
> [!CAUTION]
> Há um limite no comprimento do nome de uma instância do contador de desempenho. Quando um nome de instância de contador de Windows Communication Foundation (WCF) excede o comprimento máximo, o WCF substitui uma parte do nome da instância por um valor de hash.  
  
## <a name="see-also"></a>Consulte também

- [Contadores de desempenho](index.md)
