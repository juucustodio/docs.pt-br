---
description: 'Saiba mais sobre o método: ICorProfilerCallback4:: GetReJITParameters'
title: Método ICorProfilerCallback4::GetReJITParameters
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.GetReJITParameters
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::GetReJITParameters
helpviewer_keywords:
- ICorProfilerCallback4::GetReJITParameters method [.NET Framework profiling]
- GetReJITParameters method, ICorProfilerCallback4 interface [.NET Framework profiling]
ms.assetid: 0e9bfe07-9f20-498c-b568-9017c8f6056c
topic_type:
- apiref
ms.openlocfilehash: f8dbf2c6ae80e41b8427fdaf0ef617a83138bb14
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99788755"
---
# <a name="icorprofilercallback4getrejitparameters-method"></a>Método ICorProfilerCallback4::GetReJITParameters

Permite que o criador de perfil de código defina sinalizadores de geração de código alternativos para um novo corpo de método recompilado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetReJITParameters(     [in] ModuleID moduleId,     [in] mdMethodDef methodId,     [in] ICorProfilerFunctionControl *pFunctionControl);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `moduleID`  
 no O módulo que contém o método para o qual o CLR precisa de parâmetros de recompilação JIT.  
  
 `methodId`  
 no O `MethodDef` do método para o qual o CLR precisa de parâmetros de recompilação JIT.  
  
 `pFunctionControl`  
 no Um ponteiro para uma interface [ICorProfilerFunctionControl](icorprofilerfunctioncontrol-interface.md) que o criador de perfil pode usar para fornecer informações de recompilação JIT para o método que está sendo recompilado.  
  
## <a name="remarks"></a>Comentários  

 O CLR emite um `GetReJITParameters` retorno de chamada para que o criador de perfil possa especificar os parâmetros para a recompilação de um determinado método. O `GetReJITParameters` retorno de chamada é emitido apenas uma vez por função; os parâmetros fornecidos pelo criador de perfil se aplicam a todas as instâncias dessa função.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Interface ICorProfilerCallback4](icorprofilercallback4-interface.md)
- [Método JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md)
- [Método ReJITCompilationStarted](icorprofilercallback4-rejitcompilationstarted-method.md)
