---
description: 'Saiba mais sobre o método: IHostSyncManager:: CreateAutoEvent'
title: Método IHostSyncManager::CreateAutoEvent
ms.date: 03/30/2017
api_name:
- IHostSyncManager.CreateAutoEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSyncManager::CreateAutoEvent
helpviewer_keywords:
- IHostSyncManager::CreateAutoEvent method [.NET Framework hosting]
- CreateAutoEvent method [.NET Framework hosting]
ms.assetid: 3153643e-cf5c-4b44-8e0e-c2b22cb08208
topic_type:
- apiref
ms.openlocfilehash: 69767f1e01ead93c874eecf01c3167a5dc0e4b82
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784841"
---
# <a name="ihostsyncmanagercreateautoevent-method"></a>Método IHostSyncManager::CreateAutoEvent

Cria um objeto de evento de redefinição automática.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateAutoEvent (  
    [out] IHostAutoEvent **ppEvent  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppEvent`  
 fora Um ponteiro para o endereço de uma instância de [IHostAutoEvent](ihostautoevent-interface.md) implementada pelo host ou NULL se o objeto de evento não pôde ser criado.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`CreateAutoEvent` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Não havia memória suficiente disponível para criar o objeto de evento solicitado.|  
  
## <a name="remarks"></a>Comentários  

 `CreateAutoEvent` Cria um objeto de evento automático cujo estado é alterado automaticamente para não sinalizado após o lançamento do thread em espera. Esse método espelha a função do Win32 `CreateEvent` com um valor de `false` especificado para o `bManualReset` parâmetro  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRSyncManager](iclrsyncmanager-interface.md)
- [Interface IHostAutoEvent](ihostautoevent-interface.md)
- [Interface IHostControl](ihostcontrol-interface.md)
- [Interface IHostSyncManager](ihostsyncmanager-interface.md)
