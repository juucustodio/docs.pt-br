---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: RuntimeSuspendAborted'
title: Método ICorProfilerCallback::RuntimeSuspendAborted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RuntimeSuspendAborted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RuntimeSuspendAborted
helpviewer_keywords:
- ICorProfilerCallback::RuntimeSuspendAborted method [.NET Framework profiling]
- RuntimeSuspendAborted method [.NET Framework profiling]
ms.assetid: 5a8a4277-345b-448b-a028-fc8cff9998aa
topic_type:
- apiref
ms.openlocfilehash: 892de7ce0b4537f5526a58b6e70f66cd295be2df
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99788820"
---
# <a name="icorprofilercallbackruntimesuspendaborted-method"></a>Método ICorProfilerCallback::RuntimeSuspendAborted

Notifica o criador de perfil de que o tempo de execução anulou a suspensão de tempo de execução que estava ocorrendo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT RuntimeSuspendAborted();  
```  
  
## <a name="remarks"></a>Comentários  

 A suspensão de tempo de execução poderá ser anulada se dois threads tentarem suspender simultaneamente o tempo de execução.  
  
 O retorno de chamada [ICorProfilerCallback:: RuntimeSuspendFinished](icorprofilercallback-runtimesuspendfinished-method.md) ou o `RuntimeSuspendAborted` retorno de chamada ocorrerá em um único thread após um retorno de chamada [ICorProfilerCallback:: RuntimeSuspendStarted](icorprofilercallback-runtimesuspendstarted-method.md) .  
  
 `RuntimeSuspendAborted`É garantido que o retorno de chamada ocorra no mesmo thread que o `RuntimeSuspendStarted` retorno de chamada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
