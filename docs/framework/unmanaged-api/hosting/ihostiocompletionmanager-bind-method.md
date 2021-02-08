---
description: 'Saiba mais sobre o método: IHostIoCompletionManager:: bind'
title: Método IHostIoCompletionManager::Bind
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.Bind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::Bind
helpviewer_keywords:
- IHostIoCompletionManager::Bind method [.NET Framework hosting]
- Bind method [.NET Framework hosting]
ms.assetid: acd74cb5-7e22-4a07-83c3-82288e1abd9f
topic_type:
- apiref
ms.openlocfilehash: 2105bf06c23f70588d0c1bc0cd849b8e810d121e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784854"
---
# <a name="ihostiocompletionmanagerbind-method"></a>Método IHostIoCompletionManager::Bind

Associa o identificador especificado a uma porta de conclusão de e/s que foi criada por uma chamada anterior ao [CreateIoCompletionPort](ihostiocompletionmanager-createiocompletionport-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Bind (  
    [in] HANDLE hPort,  
    [in] HANDLE hHandle  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `hPort`  
 no A porta de conclusão de e/s à qual associar `hHandle` . Se o valor de `hPort` for NULL, `hHandle` será associado à porta de conclusão de e/s padrão.  
  
 `hHandle`  
 no O identificador do sistema operacional a ser associado `hPort` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`Bind` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Uma porta de conclusão de e/s é criada usando uma chamada para `CreateIoCompletionPort` . O CLR chama `Bind` para associar um identificador a essa porta.  
  
> [!NOTE]
> Quando uma solicitação de e/s é concluída, o host deve chamar o método [ICLRIoCompletionManager:: OnComplete](iclriocompletionmanager-oncomplete-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRIoCompletionManager](iclriocompletionmanager-interface.md)
