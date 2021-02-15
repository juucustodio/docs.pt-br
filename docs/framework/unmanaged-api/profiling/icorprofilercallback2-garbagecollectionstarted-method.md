---
description: 'Saiba mais sobre o método: ICorProfilerCallback2:: GarbageCollectionStarted'
title: Método ICorProfilerCallback2::GarbageCollectionStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.GarbageCollectionStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::GarbageCollectionStarted
helpviewer_keywords:
- GarbageCollectionStarted method [.NET Framework profiling]
- ICorProfilerCallback2::GarbageCollectionStarted method [.NET Framework profiling]
ms.assetid: 44eef087-f21f-4fe2-b481-f8a0ee022e7d
topic_type:
- apiref
ms.openlocfilehash: 2b57a21dc3a1751b5d4767ea940f64df61af4318
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647876"
---
# <a name="icorprofilercallback2garbagecollectionstarted-method"></a>Método ICorProfilerCallback2::GarbageCollectionStarted

Notifica o criador de perfil de código que a coleta de lixo foi iniciada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GarbageCollectionStarted(  
    [in] int cGenerations,  
    [in, size_is(cGenerations), length_is(cGenerations)] BOOL generationCollected[],  
    [in] COR_PRF_GC_REASON reason);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cGenerations`  
 no O número total de entradas na `generationCollected` matriz.  
  
 `generationCollected`  
 no Uma matriz de valores Boolianos, que `true` se a geração que corresponde ao índice de matriz está sendo coletada por essa coleta de lixo; caso contrário, `false` .  
  
 A matriz é indexada por um valor da enumeração [COR_PRF_GC_GENERATION](cor-prf-gc-generation-enumeration.md) , que indica a geração.  
  
 `reason`  
 no Um valor da enumeração [COR_PRF_GC_REASON](cor-prf-gc-reason-enumeration.md) que indica o motivo pelo qual a coleta de lixo foi induzida.  
  
## <a name="remarks"></a>Comentários  

 Todos os retornos de chamada que pertencem a essa coleta de lixo ocorrerão entre o `GarbageCollectionStarted` retorno de chamada e o retorno de chamada [ICorProfilerCallback2:: GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md) correspondente. Esses retornos de chamada não precisam ocorrer no mesmo thread.  
  
 É seguro que o criador de perfil Inspecione objetos em seus locais originais durante o `GarbageCollectionStarted` retorno de chamada. O coletor de lixo começará a mover objetos após o retorno de `GarbageCollectionStarted` . Depois que o criador de perfil for retornado desse retorno de chamada, o criador de perfil deverá considerar que todas as IDs de objeto sejam inválidas até receber um `ICorProfilerCallback2::GarbageCollectionFinished` retorno de chamada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Interface ICorProfilerCallback2](icorprofilercallback2-interface.md)
