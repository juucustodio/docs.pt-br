---
description: 'Saiba mais sobre o método: IHostIoCompletionManager:: CreateIoCompletionPort'
title: Método IHostIoCompletionManager::CreateIoCompletionPort
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.CreateIoCompletionPort
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::CreateIoCompletionPort
helpviewer_keywords:
- IHostIoCompletionManager::CreateIoCompletionPort method [.NET Framework hosting]
- CreateIoCompletionPort method [.NET Framework hosting]
ms.assetid: 907a2b43-68db-44a7-acac-89e792e7bb3c
topic_type:
- apiref
ms.openlocfilehash: da4cd595e84c341eb15837ff97f4ba23cac23210
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789431"
---
# <a name="ihostiocompletionmanagercreateiocompletionport-method"></a>Método IHostIoCompletionManager::CreateIoCompletionPort

Solicita que o host crie uma nova porta de conclusão de e/s.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateIoCompletionPort (  
    [out] HANDLE *phPort  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `phPort`  
 fora Um ponteiro para um identificador para a porta de conclusão de e/s recém-criada ou 0 (zero), se a porta não pôde ser criada.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`CreateIoCompletionPort` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Não havia memória suficiente disponível para alocar o recurso solicitado.|  
  
## <a name="remarks"></a>Comentários  

 O CLR chama o `CreateIoCompletionPort` método para solicitar que o host crie uma nova porta de conclusão de e/s. Ele associa as operações de e/s a essa porta por meio de uma chamada para o método [IHostIoCompletionManager:: bind](ihostiocompletionmanager-bind-method.md) . O host relata o status de volta para o CLR chamando [ICLRIoCompletionManager:: OnComplete](iclriocompletionmanager-oncomplete-method.md).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRIoCompletionManager](iclriocompletionmanager-interface.md)
- [Interface IHostIoCompletionManager](ihostiocompletionmanager-interface.md)
