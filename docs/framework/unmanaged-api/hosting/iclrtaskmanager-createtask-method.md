---
description: 'Saiba mais sobre o método: ICLRTaskManager:: CreateTask'
title: Método ICLRTaskManager::CreateTask
ms.date: 03/30/2017
api_name:
- ICLRTaskManager.CreateTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTaskManager::CreateTask
helpviewer_keywords:
- ICLRTaskManager::CreateTask method [.NET Framework hosting]
- CreateTask method, ICLRTaskManager interface [.NET Framework hosting]
ms.assetid: eea570d9-2e53-4320-9ea0-eb777bf9dcf3
topic_type:
- apiref
ms.openlocfilehash: 98a287f10a84b18579ebf2a4294cbb8a67cabc9c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728607"
---
# <a name="iclrtaskmanagercreatetask-method"></a>Método ICLRTaskManager::CreateTask

Solicitações explicitamente que o Common Language Runtime (CLR) cria uma nova tarefa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateTask (  
    [out] ICLRTask **pTask  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pTask`  
 fora Um ponteiro para o endereço de um [ICLRTask](iclrtask-interface.md)recém-criado, ou NULL, se a tarefa não pôde ser criada.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Não há memória suficiente disponível para alocar o recurso solicitado.|  
  
## <a name="remarks"></a>Comentários  

 O CLR cria uma nova tarefa automaticamente na inicialização, quando o código do usuário cria um thread usando tipos no <xref:System.Threading> namespace ou quando o tamanho do pool de threads é aumentado. Ele também cria tarefas quando o código não gerenciado faz uma chamada para uma função gerenciada.  
  
 `CreateTask` permite que o host faça uma solicitação explícita de que o CLR crie uma nova tarefa. Por exemplo, o host pode invocar esse método para inicializar as estruturas de dados.  
  
> [!IMPORTANT]
> A nova tarefa é retornada em um estado suspenso e permanece suspensa até que o host chame explicitamente [IHostTask:: Start](ihosttask-start-method.md).  
  
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
