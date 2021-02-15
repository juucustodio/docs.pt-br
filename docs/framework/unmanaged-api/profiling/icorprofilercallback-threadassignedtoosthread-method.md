---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ThreadAssignedToOSThread'
title: Método ICorProfilerCallback::ThreadAssignedToOSThread
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ThreadAssignedToOSThread
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ThreadAssignedToOSThread
helpviewer_keywords:
- ThreadAssignedToOSThread method [.NET Framework profiling]
- ICorProfilerCallback::ThreadAssignedToOSThread method [.NET Framework profiling]
ms.assetid: f9671e5a-7b14-4f5b-8404-58136422c8b2
topic_type:
- apiref
ms.openlocfilehash: 04fba4cabb0ac58b3afeaae1fd579865335a9e14
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647971"
---
# <a name="icorprofilercallbackthreadassignedtoosthread-method"></a>Método ICorProfilerCallback::ThreadAssignedToOSThread

Notifica o criador de perfil de que um thread gerenciado está sendo implementado usando um determinado thread do sistema operacional.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ThreadAssignedToOSThread(  
    [in] ThreadID managedThreadId,  
    [in] DWORD    osThreadId);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `managedThreadId`  
 no O identificador do thread gerenciado.  
  
 `osThreadId`  
 no O identificador do thread do sistema operacional.  
  
## <a name="remarks"></a>Comentários  

 O `ThreadAssignedToOSThread` retorno de chamada existe para que o criador de perfil possa manter um mapeamento preciso entre fibras de threads do sistema operacional para threads gerenciados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
