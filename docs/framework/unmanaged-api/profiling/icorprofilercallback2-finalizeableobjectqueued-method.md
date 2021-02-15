---
description: 'Saiba mais sobre o método: ICorProfilerCallback2:: FinalizeableObjectQueued'
title: Método ICorProfilerCallback2::FinalizeableObjectQueued
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.FinalizeableObjectQueued
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::FinalizeableObjectQueued
helpviewer_keywords:
- FinalizeableObjectQueued method [.NET Framework profiling]
- ICorProfilerCallback2::FinalizeableObjectQueued method [.NET Framework profiling]
ms.assetid: 92d76893-683c-475d-9996-5bff03cdb10f
topic_type:
- apiref
ms.openlocfilehash: 62424ea60f72cee2328a143e4e50acd7af33e221
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647902"
---
# <a name="icorprofilercallback2finalizeableobjectqueued-method"></a>Método ICorProfilerCallback2::FinalizeableObjectQueued

Notifica o criador de perfil de código de que um objeto com um finalizador foi enfileirado para o thread do finalizador para execução de seu `Finalize` método.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FinalizeableObjectQueued(  
    [in] DWORD finalizerFlags,  
    [in] ObjectID objectID);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `finalizerFlags`  
 no Um valor da enumeração [COR_PRF_FINALIZER_FLAGS](cor-prf-finalizer-flags-enumeration.md) que descreve os aspectos do finalizador.  
  
 `objectID`  
 no A ID do objeto que foi enfileirado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Interface ICorProfilerCallback2](icorprofilercallback2-interface.md)
