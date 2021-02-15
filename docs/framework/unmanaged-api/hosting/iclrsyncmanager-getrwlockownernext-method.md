---
description: 'Saiba mais sobre o método: ICLRSyncManager:: GetRWLockOwnerNext'
title: Método ICLRSyncManager::GetRWLockOwnerNext
ms.date: 03/30/2017
api_name:
- ICLRSyncManager.GetRWLockOwnerNext
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRSyncManager::GetRWLockOwnerNext
helpviewer_keywords:
- ICLRSyncManager::GetRWLockOwnerNext method [.NET Framework hosting]
- GetRWLockOwnerNext method [.NET Framework hosting]
ms.assetid: 0e025b6a-280e-40a2-a2d0-b15f58777b81
topic_type:
- apiref
ms.openlocfilehash: f49bdd5065ac896147967c0a013347ab39ce1eff
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784984"
---
# <a name="iclrsyncmanagergetrwlockownernext-method"></a>Método ICLRSyncManager::GetRWLockOwnerNext

Obtém a próxima instância de [IHostTask](ihosttask-interface.md) que está bloqueada no bloqueio leitor-gravador atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetRWLockOwnerNext (  
    [in] SIZE_T       Iterator,  
    [out] IHostTask  *ppOwnerHostTask  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `Iterator`  
 no O iterador criado usando uma chamada para [CreateRWLockOwnerIterator](iclrsyncmanager-createrwlockowneriterator-method.md).  
  
 `ppOwnerHostTask`  
 fora Um ponteiro para o próximo `IHostTask` que está aguardando o bloqueio ou nulo se nenhuma tarefa estiver aguardando.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`GetRWLockOwnerNext` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Se `ppOwnerHostTask` é definido como NULL, a iteração foi encerrada e o host deve chamar o método [DeleteRWLockOwnerIterator](iclrsyncmanager-deleterwlockowneriterator-method.md) .  
  
> [!NOTE]
> O CLR chama `AddRef` o `IHostTask` para o qual `ppOwnerHostTask` aponta para impedir que essa tarefa saia enquanto o host mantém o ponteiro. O host deve chamar `Release` para diminuir a contagem de referência quando for concluído.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRSyncManager](iclrsyncmanager-interface.md)
- [Interface IHostSyncManager](ihostsyncmanager-interface.md)
