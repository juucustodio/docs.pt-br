---
description: 'Saiba mais sobre: interface IHostThreadPoolManager'
title: Interface IHostThreadPoolManager
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager
helpviewer_keywords:
- IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: c3a2cd90-7c4e-4374-bb87-b41befb8344f
topic_type:
- apiref
ms.openlocfilehash: 0361b7a08f781a8748e43959f65ce0e9f21bbac1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728392"
---
# <a name="ihostthreadpoolmanager-interface"></a>Interface IHostThreadPoolManager

Fornece métodos que permitem que o Common Language Runtime (CLR) Configure o pool de threads e enfileirar itens de trabalho para o pool de threads.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetAvailableThreads](ihostthreadpoolmanager-getavailablethreads-method.md)|Obtém o número de threads no pool de threads que não estão processando itens de trabalho no momento.|  
|[Método GetMaxThreads](ihostthreadpoolmanager-getmaxthreads-method.md)|Obtém o número máximo de threads que o host mantém simultaneamente no pool de threads.|  
|[Método GetMinThreads](ihostthreadpoolmanager-getminthreads-method.md)|Obtém o número mínimo de threads ociosos que o host mantém em antecipação de solicitações.|  
|[Método QueueUserWorkItem](ihostthreadpoolmanager-queueuserworkitem-method.md)|Enfileira uma função para execução e fornece um objeto que contém dados a serem usados pela função.|  
|[Método SetMaxThreads](ihostthreadpoolmanager-setmaxthreads-method.md)|Define o número máximo de threads que o host pode manter no pool de threads.|  
|[Método SetMinThreads](ihostthreadpoolmanager-setminthreads-method.md)|Define o número mínimo de threads ociosos que o host deve manter em antecipação de solicitações.|  
  
## <a name="remarks"></a>Comentários  

 O host não é necessário para configurar o pool de threads usando os valores especificados em chamadas para `SetMaxThreads` os `SetMinThreads` métodos e. Nesse caso, o host deve retornar um valor HRESULT de E_NOTIMPL desses métodos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Threading>
- <xref:System.Threading.ThreadPool>
- [Interfaces de hospedagem](hosting-interfaces.md)
