---
description: 'Saiba mais sobre o método: ICLRTask:: NeedsPriorityScheduling'
title: Método ICLRTask::NeedsPriorityScheduling
ms.date: 03/30/2017
api_name:
- ICLRTask.NeedsPriorityScheduling
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask::NeedsPriorityScheduling
helpviewer_keywords:
- ICLRTask::NeedsPriorityScheduling method [.NET Framework hosting]
- NeedsPriorityScheduling method [.NET Framework hosting]
ms.assetid: 9c9db3f3-26bf-4317-88de-5eb926a22a1d
topic_type:
- apiref
ms.openlocfilehash: e6e1b93b38d86259dc2f405f8512ec1063fe7b3b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781760"
---
# <a name="iclrtaskneedspriorityscheduling-method"></a>Método ICLRTask::NeedsPriorityScheduling

Obtém um valor que indica se a tarefa atual, que está sendo desativada, precisa ser marcada como uma prioridade alta para reagendar.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT NeedsPriorityScheduling (  
    [out] BOOL *pbNeedsPriorityScheduling  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbNeedsPriorityRescheduling`  
 [fora] `true` , se o host deve tentar reagendar a instância de tarefa atual assim que possível; caso contrário, `false` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`NeedsPriorityRescheduling` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Em situações em que a tarefa está próxima de ser coletada pelo coletor de lixo, o CLR define o valor de `pbNeedsPriorityScheduling` como `true` , indicando reagendamento de alta prioridade. Isso permite que o host reagende a tarefa rapidamente, minimizando assim o potencial de atrasos na coleta de lixo e permitindo que o host e o tempo de execução cooperam em conservar recursos de memória.  
  
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
