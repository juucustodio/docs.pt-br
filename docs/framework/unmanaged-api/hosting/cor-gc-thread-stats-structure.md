---
description: 'Saiba mais sobre: estrutura de COR_GC_THREAD_STATS'
title: Estrutura COR_GC_THREAD_STATS
ms.date: 03/30/2017
api_name:
- COR_GC_THREAD_STATS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_THREAD_STATS
helpviewer_keywords:
- COR_GC_THREAD_STATS structure [.NET Framework hosting]
ms.assetid: 01f9a59b-7679-4d42-9ced-4a8981625c3d
topic_type:
- apiref
ms.openlocfilehash: 179eb335e9f8c118ee98d4b777c347f3758ee0c6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799779"
---
# <a name="cor_gc_thread_stats-structure"></a>Estrutura COR_GC_THREAD_STATS

Contém estatísticas por thread referentes à coleta de lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _COR_GC_THREAD_STATS {  
    ULONGLONG  PerThreadAllocation;
    ULONG      Flags;
} COR_GC_THREAD_STATS;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`PerThreadAllocation`|O número de bytes de memória alocados no thread que está associado à instância atual `COR_GC_THREAD_STATS` . Esse número é limpo para zero sempre que uma coleta de lixo de geração zero ocorre.|  
|`Flags`|O número de bytes promovidos para uma geração mais alta na coleta de lixo mais recente.|  
  
## <a name="remarks"></a>Comentários  

 [ICLRTask:: GetMemStats](iclrtask-getmemstats-method.md) usa um parâmetro de saída do tipo `COR_GC_THREAD_STATS` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** GCHost. idl  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de hospedagem](hosting-structures.md)
- [Interface IHostTask](ihosttask-interface.md)
