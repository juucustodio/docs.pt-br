---
description: 'Saiba mais sobre o método: ICorProfilerCallback2:: GarbageCollectionFinished'
title: Método ICorProfilerCallback2::GarbageCollectionFinished
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.GarbageCollectionFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::GarbageCollectionFinished
helpviewer_keywords:
- ICorProfilerCallback2::GarbageCollectionFinished method [.NET Framework profiling]
- GarbageCollectionFinished method [.NET Framework profiling]
ms.assetid: 1a5758ea-2354-43c0-92a3-32c9909d64e1
topic_type:
- apiref
ms.openlocfilehash: 9e41c5ced76af40866269fdff74fd302b937b70e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99657106"
---
# <a name="icorprofilercallback2garbagecollectionfinished-method"></a>Método ICorProfilerCallback2::GarbageCollectionFinished

Notifica o criador de perfil de que a coleta de lixo foi concluída e que todos os retornos de chamada de coleta de lixo foram emitidos para ela.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GarbageCollectionFinished();  
```  
  
## <a name="remarks"></a>Comentários  

 É seguro que o criador de perfil Inspecione objetos em seus locais finais quando o `GarbageCollectionFinished` método é chamado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Interface ICorProfilerCallback2](icorprofilercallback2-interface.md)
