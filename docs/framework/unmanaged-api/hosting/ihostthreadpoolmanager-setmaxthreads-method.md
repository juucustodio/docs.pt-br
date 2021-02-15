---
description: 'Saiba mais sobre o método: IHostThreadPoolManager:: SetMaxThreads'
title: Método IHostThreadPoolManager::SetMaxThreads
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager.SetMaxThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager::SetMaxThreads
helpviewer_keywords:
- IHostThreadPoolManager::SetMaxThreads method [.NET Framework hosting]
- SetMaxThreads method, IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: 77cfd347-95c2-4425-b807-4ecc2a8d4578
topic_type:
- apiref
ms.openlocfilehash: 83266b05f639c0aa63e492bca525cbbf09a30775
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99671237"
---
# <a name="ihostthreadpoolmanagersetmaxthreads-method"></a>Método IHostThreadPoolManager::SetMaxThreads

Define o número máximo de threads que o host pode manter no pool de threads.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetMaxThreads (  
    [in] DWORD MaxThreads  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `MaxThreads`  
 O número máximo de threads de trabalho no pool de threads.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`SetMaxThreads` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_NOTIMPL|O host não fornece uma implementação de `SetMaxThreads` .|  
  
## <a name="remarks"></a>Comentários  

 Não é necessário um host para permitir que o CLR configure o tamanho do pool de threads. Alguns hosts podem querer um controle exclusivo sobre o pool de threads, por motivos como implementação, desempenho ou escalabilidade. Nesse caso, um host deve retornar um valor HRESULT de E_NOTIMPL.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Threading.ThreadPool.SetMaxThreads%2A>
- <xref:System.Threading.ThreadPool>
- [Método GetMaxThreads](ihostthreadpoolmanager-getmaxthreads-method.md)
- [Método SetMinThreads](ihostthreadpoolmanager-setminthreads-method.md)
- [Interface IHostThreadPoolManager](ihostthreadpoolmanager-interface.md)
