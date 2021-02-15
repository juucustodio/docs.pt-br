---
description: 'Saiba mais sobre o método: IHostSyncManager:: CreateRWLockWriterEvent'
title: Método IHostSyncManager::CreateRWLockWriterEvent
ms.date: 03/30/2017
api_name:
- IHostSyncManager.CreateRWLockWriterEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSyncManager::CreateRWLockWriterEvent
helpviewer_keywords:
- CreateRWLockWriterEvent method [.NET Framework hosting]
- IHostSyncManager::CreateRWLockWriterEvent method [.NET Framework hosting]
ms.assetid: 70e488c2-cf53-4dc0-ba52-74372d215c41
topic_type:
- apiref
ms.openlocfilehash: 509f18ff49966e5da3a25e39258d33caf69249a0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784750"
---
# <a name="ihostsyncmanagercreaterwlockwriterevent-method"></a>Método IHostSyncManager::CreateRWLockWriterEvent

Cria um objeto de evento de redefinição automática para a implementação de um bloqueio de gravador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateRWLockWriterEvent (  
    [in]  SIZE_T cookie,  
    [out] IHostAutoEvent **ppEvent  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cookie`  
 no Um cookie a ser associado ao evento de redefinição automática.  
  
 `ppEvent`  
 fora Um ponteiro para o endereço de uma instância de [IHostAutoEvent](ihostautoevent-interface.md) ou NULL se o objeto de evento não pôde ser criado.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`CreateRWLockWriterEvent` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Não havia memória suficiente disponível para criar o objeto de evento solicitado.|  
  
## <a name="remarks"></a>Comentários  

 O CLR chama o `CreateRWLockWriterEvent` método para obter uma referência a uma `IHostAutoEvent` instância a ser usada em sua implementação de um bloqueio de gravador. O host pode usar o cookie especificado para determinar quais tarefas estão aguardando no bloqueio chamando os métodos de iteração da interface [ICLRSyncManager](iclrsyncmanager-interface.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRSyncManager](iclrsyncmanager-interface.md)
- [Interface IHostAutoEvent](ihostautoevent-interface.md)
- [Interface IHostManualEvent](ihostmanualevent-interface.md)
- [Interface IHostSyncManager](ihostsyncmanager-interface.md)
