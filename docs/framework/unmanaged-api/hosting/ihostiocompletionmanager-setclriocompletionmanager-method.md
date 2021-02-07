---
description: 'Saiba mais sobre o método: IHostIoCompletionManager:: SetCLRIoCompletionManager'
title: Método IHostIoCompletionManager::SetCLRIoCompletionManager
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.SetCLRIoCompletionManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::SetCLRIoCompletionManager
helpviewer_keywords:
- IHostIoCompletionManager::SetCLRIoCompletionManager method [.NET Framework hosting]
- SetCLRIoCompletionManager method [.NET Framework hosting]
ms.assetid: 4254bb01-3a14-4f34-a3be-60ff1f5072b5
topic_type:
- apiref
ms.openlocfilehash: 1075c33d6de4f5edf34364d67cbc0a21c4f19802
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99708288"
---
# <a name="ihostiocompletionmanagersetclriocompletionmanager-method"></a>Método IHostIoCompletionManager::SetCLRIoCompletionManager

Fornece ao host um ponteiro de interface para a instância [ICLRIoCompletionManager](iclriocompletionmanager-interface.md) implementada pelo Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetCLRIoCompletionManager (  
    [in] ICLRIoCompletionManager *pManager  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pManager`  
 no Um ponteiro de interface para uma `ICLRIoCompletionManager` instância fornecida pelo CLR.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`SetCLRIoCompletionManager` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Depois que o CLR tiver sido chamado `SetCLRIoCompletionManager` , o host deverá chamar [ICLRIoCompletionManager:: OnComplete](iclriocompletionmanager-oncomplete-method.md) para notificar o CLR quando uma solicitação de e/s for concluída.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRIoCompletionManager](iclriocompletionmanager-interface.md)
- [Interface IHostIoCompletionManager](ihostiocompletionmanager-interface.md)
