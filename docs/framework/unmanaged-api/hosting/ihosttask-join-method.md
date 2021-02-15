---
description: 'Saiba mais sobre o método: IHostTask:: join'
title: Método IHostTask::Join
ms.date: 03/30/2017
api_name:
- IHostTask.Join
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask::Join
helpviewer_keywords:
- IHostTask::Join method [.NET Framework hosting]
- Join method, IHostTask interface [.NET Framework hosting]
ms.assetid: 2cffcc52-19e0-4ced-a440-fc7375078ac9
topic_type:
- apiref
ms.openlocfilehash: 8231401ab01ee040f225b78a52b61eb7d59af1d7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784646"
---
# <a name="ihosttaskjoin-method"></a>Método IHostTask::Join

Bloqueia a tarefa de chamada até que a tarefa representada pela instância [IHostTask](ihosttask-interface.md) atual seja concluída, o intervalo de tempo especificado decorre ou [IHostTask:: Alert](ihosttask-alert-method.md) seja chamado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Join (  
    [in] DWORD milliseconds,  
    [in] DWORD option  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `milliseconds`  
 no O intervalo de tempo, em milissegundos, para aguardar até que a tarefa seja encerrada. Se esse intervalo expirar antes da tarefa ser encerrada, a tarefa de chamada desbloqueará.  
  
 `option`  
 no Um dos valores de [WAIT_OPTION](wait-option-enumeration.md) . Um valor de WAIT_ALERTABLE instrui o host a ativar a tarefa se `Alert` for chamado antes de `milliseconds` decorrer.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`Join` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava aguardando, ou a `IHostTask` instância atual não está associada a uma tarefa.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
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
- [Enumeração WAIT_OPTION](wait-option-enumeration.md)
