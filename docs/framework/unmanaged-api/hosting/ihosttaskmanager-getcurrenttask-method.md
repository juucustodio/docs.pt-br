---
description: 'Saiba mais sobre o método: IHostTaskManager:: GetCurrentTask'
title: Método IHostTaskManager::GetCurrentTask
ms.date: 03/30/2017
api_name:
- IHostTaskManager.GetCurrentTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::GetCurrentTask
helpviewer_keywords:
- GetCurrentTask method, IHostTaskManager interface [.NET Framework hosting]
- IHostTaskManager::GetCurrentTask method [.NET Framework hosting]
ms.assetid: f17bca49-90bd-4dee-a5e1-b9a57ea46f85
topic_type:
- apiref
ms.openlocfilehash: 7e7e516fe4a706fce8b0302f318cfbb164a86eea
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753803"
---
# <a name="ihosttaskmanagergetcurrenttask-method"></a>Método IHostTaskManager::GetCurrentTask

Obtém um ponteiro de interface para a tarefa que está atualmente em execução no thread do sistema operacional do qual essa chamada é feita.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCurrentTask (  
    [out] IHostTask **pTask  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pTask`  
 fora Um ponteiro para o endereço de uma instância de [IHostTask](ihosttask-interface.md) que representa a tarefa em execução no momento, ou NULL, se nenhuma tarefa estiver em execução no momento.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`GetCurrentTask` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_INVALIDOPERATION|`GetCurrentTask` foi chamado em um thread do sistema operacional fora do controle do host.|  
  
## <a name="remarks"></a>Comentários  

 O host também pode definir o `pTask` parâmetro como nulo para impedir que uma tarefa que não foi iniciada Insira o CLR.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRTask](iclrtask-interface.md)
- [Interface ICLRTaskManager](iclrtaskmanager-interface.md)
- [Interface IHostTask](ihosttask-interface.md)
- [Interface IHostTaskManager](ihosttaskmanager-interface.md)
