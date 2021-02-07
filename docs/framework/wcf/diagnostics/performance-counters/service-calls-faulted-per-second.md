---
description: 'Saiba mais sobre: Service: chamadas com falha por segundo'
title: 'Serviço: chamadas com falha por segundo'
ms.date: 03/30/2017
ms.assetid: 94247356-2b29-4b50-b639-91ca8c1cf3a9
ms.openlocfilehash: 87b4ec8a6868f2694f7aefa34d977e618db16e16
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99705415"
---
# <a name="service-calls-faulted-per-second"></a>Serviço: chamadas com falha por segundo

Nome do contador: chamadas com falha por segundo.  
  
## <a name="description"></a>Descrição  

 Número de chamadas que retornaram falhas para esse serviço em um segundo.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)  
  
 Em aplicativos Windows Communication Foundation (WCF), os métodos de serviço comunicam informações de erro de processamento usando mensagens de falha SOAP. Falhas de SOAP são tipos de mensagem que são incluídos nos metadados de uma operação de serviço e, portanto, criam um contrato de falha que os clientes podem usar para tornar sua execução mais robusta ou interativa. Como as falhas de SOAP são expressas para clientes em formato XML, elas são altamente interoperáveis.  
  
## <a name="see-also"></a>Consulte também

- [Especificando e lidando com falhas em contratos e serviços](../../specifying-and-handling-faults-in-contracts-and-services.md)
