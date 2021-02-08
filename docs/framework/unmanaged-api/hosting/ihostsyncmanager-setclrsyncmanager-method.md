---
description: 'Saiba mais sobre o método: IHostSyncManager:: SetCLRSyncManager'
title: Método IHostSyncManager::SetCLRSyncManager
ms.date: 03/30/2017
api_name:
- IHostSyncManager.SetCLRSyncManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSyncManager::SetCLRSyncManager
helpviewer_keywords:
- IHostSyncManager::SetCLRSyncManager method [.NET Framework hosting]
- SetCLRSyncManager method [.NET Framework hosting]
ms.assetid: 2b8bbe76-a45d-4989-bacb-11df42f8798c
topic_type:
- apiref
ms.openlocfilehash: e2a6a54334f7b8a63696ead918f4f34e0c36e438
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784701"
---
# <a name="ihostsyncmanagersetclrsyncmanager-method"></a>Método IHostSyncManager::SetCLRSyncManager

Define a instância de [ICLRSyncManager](iclrsyncmanager-interface.md) a ser associada à instância de [IHostSyncManager](ihostsyncmanager-interface.md) atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetCLRSyncManager (  
    [in] ICLRSyncManager *pManager  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pManager`  
 no Um ponteiro para uma `ICLRSyncManager` instância fornecida pelo Common Language Runtime (CLR).  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`SetCLRSyncManager` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Para facilitar a comunicação entre o host e o CLR, as interfaces de hospedagem geralmente vêm em pares. Um membro do par é implementado pelo host e o outro membro é implementado pelo CLR. Como uma implementação do lado do host, a `IHostSyncManager` interface corresponde à `ICLRSyncManager` interface implementada pelo CLR. O CLR chama `SetCLRSyncManager` para fornecer uma `ICLRSyncManager` instância para que o host seja associado à `IHostSyncManager` instância atual.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRSyncManager](iclrsyncmanager-interface.md)
- [Interface IHostSyncManager](ihostsyncmanager-interface.md)
