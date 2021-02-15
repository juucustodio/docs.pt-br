---
description: 'Saiba mais sobre: método IHostManualEvent:: Set'
title: Método IHostManualEvent::Set
ms.date: 03/30/2017
api_name:
- IHostManualEvent.Set
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostManualEvent::Set
helpviewer_keywords:
- Set method, IHostManualEvent interface [.NET Framework hosting]
- IHostManualEvent::Set method [.NET Framework hosting]
ms.assetid: e930c174-f71d-4faa-bb59-f0fb3df4d77b
topic_type:
- apiref
ms.openlocfilehash: e2de1fde2f8c0f512733ecde43d5240a94f84264
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99707924"
---
# <a name="ihostmanualeventset-method"></a>Método IHostManualEvent::Set

Define a instância de [IHostManualEvent](ihostmanualevent-interface.md) atual para um estado sinalizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Set ();  
```  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`Set` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRSyncManager](iclrsyncmanager-interface.md)
- [Interface IHostAutoEvent](ihostautoevent-interface.md)
- [Interface IHostManualEvent](ihostmanualevent-interface.md)
- [Interface IHostSemaphore](ihostsemaphore-interface.md)
- [Interface IHostSyncManager](ihostsyncmanager-interface.md)
