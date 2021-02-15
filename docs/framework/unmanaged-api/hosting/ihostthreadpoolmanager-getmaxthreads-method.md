---
description: 'Saiba mais sobre o método: IHostThreadPoolManager:: GetMaxThreads'
title: Método IHostThreadPoolManager::GetMaxThreads
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager.GetMaxThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager::GetMaxThreads
helpviewer_keywords:
- IHostThreadPoolManager::GetMaxThreads method [.NET Framework hosting]
- GetMaxThreads method, IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: db268876-6178-4a81-aca3-318ee7f96001
topic_type:
- apiref
ms.openlocfilehash: e8cae2aa29a50ef58a5b87deba9e275a441d43ef
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728360"
---
# <a name="ihostthreadpoolmanagergetmaxthreads-method"></a>Método IHostThreadPoolManager::GetMaxThreads

Obtém o número máximo de threads que o host mantém simultaneamente no pool de threads.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMaxThreads (  
    [out] DWORD *pdwMaxWorkerThreads  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pdwMaxWorkerThreads`  
 fora Um ponteiro para o número máximo de threads que o host mantém no pool de threads.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`GetMaxThreads` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR (não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_NOTIMPL|O host não fornece uma implementação de `GetMaxThreads` .|  
  
## <a name="remarks"></a>Comentários  

 O CLR chama `GetMaxThreads` para determinar o número total de threads no pool de threads. O método [GetAvailableThreads](ihostthreadpoolmanager-getavailablethreads-method.md) Obtém o número de threads que não estão processando itens de trabalho no momento. Todas as solicitações acima do valor retornado do `pdwMaxWorkerThreads` parâmetro permanecem enfileiradas até que os threads se tornem disponíveis.  
  
 Se o host não fornecer uma implementação de `GetMaxThreads` , ele deverá retornar um valor HRESULT de E_NOTIMPL.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Threading.ThreadPool.GetMaxThreads%2A>
- <xref:System.Threading.ThreadPool>
- [Método GetMinThreads](ihostthreadpoolmanager-getminthreads-method.md)
- [Método SetMaxThreads](ihostthreadpoolmanager-setmaxthreads-method.md)
- [Interface IHostThreadPoolManager](ihostthreadpoolmanager-interface.md)
