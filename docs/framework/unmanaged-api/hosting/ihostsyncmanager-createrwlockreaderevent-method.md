---
description: 'Saiba mais sobre o método: IHostSyncManager:: CreateRWLockReaderEvent'
title: Método IHostSyncManager::CreateRWLockReaderEvent
ms.date: 03/30/2017
api_name:
- IHostSyncManager.CreateRWLockReaderEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSyncManager::CreateRWLockReaderEvent
helpviewer_keywords:
- CreateRWLockReaderEvent method [.NET Framework hosting]
- IHostSyncManager::CreateRWLockReaderEvent method [.NET Framework hosting]
ms.assetid: 68c4ea19-c47c-45c6-b420-d3a2ba1c2d50
topic_type:
- apiref
ms.openlocfilehash: be20757924aa45d2a44edab9bf921026aa0247a5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784763"
---
# <a name="ihostsyncmanagercreaterwlockreaderevent-method"></a>Método IHostSyncManager::CreateRWLockReaderEvent

Cria um objeto de evento de redefinição manual para a implementação de um bloqueio de leitor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateRWLockReaderEvent (  
    [in]  BOOL bInitialState,  
    [in]  SIZE_T cookie,  
    [out] IHostManualEvent **ppEvent  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `bInitialState`  
 [in] `true` , se `ppEvent` deve ser sinalizado; caso contrário, `false` .  
  
 `cookie`  
 no Um cookie a ser associado ao bloqueio do leitor.  
  
 `ppEvent`  
 fora Um ponteiro para o endereço de uma instância de [IHostManualEvent](ihostmanualevent-interface.md) ou NULL se o objeto de evento não pôde ser criado.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`CreateRWLockReaderEvent` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Não havia memória suficiente disponível para criar o objeto de evento solicitado.|  
  
## <a name="remarks"></a>Comentários  

 O CLR chama `CreateRWLockReaderEvent` para obter uma referência a uma `IHostManualEvent` instância a ser usada na implementação de um bloqueio de leitor. O host pode usar o cookie para determinar quais tarefas estão aguardando no bloqueio do leitor consultando a interface [ICLRSyncManager](iclrsyncmanager-interface.md) .  
  
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
