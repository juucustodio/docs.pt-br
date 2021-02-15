---
description: 'Saiba mais sobre o método: ICLRIoCompletionManager:: OnComplete'
title: Método ICLRIoCompletionManager::OnComplete
ms.date: 03/30/2017
api_name:
- ICLRIoCompletionManager.OnComplete
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRIoCompletionManager::OnComplete
helpviewer_keywords:
- OnComplete method [.NET Framework hosting]
- ICLRIoCompletionManager::OnComplete method [.NET Framework hosting]
ms.assetid: 003f6974-9727-4322-bed5-e330d1224d0b
topic_type:
- apiref
ms.openlocfilehash: d54b189debdfc2959676b53fd3fb51b2c10dce17
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789873"
---
# <a name="iclriocompletionmanageroncomplete-method"></a>Método ICLRIoCompletionManager::OnComplete

Notifica o Common Language Runtime (CLR) do status de uma solicitação de e/s que foi feita usando uma chamada para o método [IHostIoCompletionManager:: bind](ihostiocompletionmanager-bind-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT OnComplete (  
    [in] DWORD dwErrorCode,  
    [in] DWORD NumberOfBytesTransferred,  
    [in] void* pvOverlapped  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwErrorCode`  
 no Um valor HRESULT que indica o status da operação de associação.  
  
- S_OK indica que a operação foi concluída com êxito.  
  
- HOST_E_INTERRUPTED indica que a chamada foi encerrada antes da conclusão.  
  
- E_FAIL indica que ocorreu uma falha catastrófica desconhecida e irrecuperável.  
  
 `NumberOfBytesTransferred`  
 no O número de bytes transferidos durante o processamento da solicitação de e/s.  
  
 `pvOverlapped`  
 no Um ponteiro para a `OVERLAPPED` estrutura que foi passada para a chamada para o `IHostIoCompletionManager::Bind` método.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`OnComplete` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Se o host implementar uma abstração de conclusão de e/s, o CLR fará solicitações de e/s por meio do host usando métodos de [IHostIoCompletionManager](ihostiocompletionmanager-interface.md). O host então chama o `OnComplete` método para notificar o tempo de execução do resultado de tais solicitações.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRIoCompletionManager](iclriocompletionmanager-interface.md)
- [Interface IHostIoCompletionManager](ihostiocompletionmanager-interface.md)
- [Interface IHostThreadPoolManager](ihostthreadpoolmanager-interface.md)
