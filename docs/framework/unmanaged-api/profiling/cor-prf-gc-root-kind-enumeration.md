---
description: 'Saiba mais sobre: enumeração de COR_PRF_GC_ROOT_KIND'
title: Enumeração COR_PRF_GC_ROOT_KIND
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_ROOT_KIND
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_ROOT_KIND
helpviewer_keywords:
- COR_PRF_GC_ROOT_KIND enumeration [.NET Framework profiling]
ms.assetid: b9fb1c03-417f-41d4-aed4-02cb4ade8def
topic_type:
- apiref
ms.openlocfilehash: 148d48458c906974d76b9e0ec0cb6b4d15ee49ef
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99648773"
---
# <a name="cor_prf_gc_root_kind-enumeration"></a>Enumeração COR_PRF_GC_ROOT_KIND

Indica o tipo de raiz de coleta de lixo que é exposta pelo retorno de chamada [ICorProfilerCallback2:: RootReferences2](icorprofilercallback2-rootreferences2-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    COR_PRF_GC_ROOT_STACK = 1,  
    COR_PRF_GC_ROOT_FINALIZER = 2,  
    COR_PRF_GC_ROOT_HANDLE = 3,  
    COR_PRF_GC_ROOT_OTHER = 0  
} COR_PRF_GC_ROOT_KIND;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`COR_PRF_GC_ROOT_STACK`|A raiz é uma variável na pilha.|  
|`COR_PRF_GC_ROOT_FINALIZER`|A raiz é uma entrada na fila do finalizador.|  
|`COR_PRF_GC_ROOT_HANDLE`|A raiz é um identificador de coleta de lixo.|  
|`COR_PRF_GC_ROOT_OTHER`|O tipo de raiz não está especificado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criando perfil de enumerações](profiling-enumerations.md)
