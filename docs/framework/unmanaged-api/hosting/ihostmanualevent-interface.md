---
description: 'Saiba mais sobre: interface IHostManualEvent'
title: Interface IHostManualEvent
ms.date: 03/30/2017
api_name:
- IHostManualEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostManualEvent
helpviewer_keywords:
- IHostManualEvent interface [.NET Framework hosting]
ms.assetid: 300c2661-b7d1-4c39-b080-9ebdef0fd523
topic_type:
- apiref
ms.openlocfilehash: 1c70935568b9ff4080fd5bcdc372c02d354aa06f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99708119"
---
# <a name="ihostmanualevent-interface"></a>Interface IHostManualEvent

Fornece a implementação do host de uma representação de um evento de redefinição manual.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Reset](ihostmanualevent-reset-method.md)|Redefine a `IHostManualEvent` instância atual para um estado não sinalizado.|  
|[Método Set](ihostmanualevent-set-method.md)|Define a `IHostManualEvent` instância atual para um estado sinalizado.|  
|[Método Wait](ihostmanualevent-wait-method.md)|Faz com que a `IHostManualEvent` instância atual aguarde até que ela seja propriedade ou uma quantidade especificada de tempo decorre.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRSyncManager](iclrsyncmanager-interface.md)
- [Interface IHostAutoEvent](ihostautoevent-interface.md)
- [Interface IHostSemaphore](ihostsemaphore-interface.md)
- [Interface IHostSyncManager](ihostsyncmanager-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
