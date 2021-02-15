---
description: 'Saiba mais sobre o método: ICorProfilerInfo4:: EnumJITedFunctions2'
title: Método ICorProfilerInfo4::EnumJITedFunctions2
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.EnumJITedFunctions2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::EnumJITedFunctions2
helpviewer_keywords:
- EnumJITedFunctions2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::EnumJITedFunctions2 method [.NET Framework profiling]
ms.assetid: 40e9a1be-9bd2-4fad-9921-34a84b61c1e3
topic_type:
- apiref
ms.openlocfilehash: 3740236cfe2bc7ecc6cd3bbeb3345c7510dd159f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686941"
---
# <a name="icorprofilerinfo4enumjitedfunctions2-method"></a>Método ICorProfilerInfo4::EnumJITedFunctions2

Retorna um enumerador para todas as funções que foram previamente compiladas e recompiladas por JIT. Esse método substitui o método [ICorProfilerInfo3:: EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md) , que não enumera IDs de compilação JIT recompiladas.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumJITedFunctions([out] ICorProfilerFunctionEnum** ppEnum);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppEnum`  
 fora Um ponteiro para o enumerador [ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md) .  
  
## <a name="remarks"></a>Comentários  

 Esse método pode se sobrepor a `JITCompilation` retornos de chamada como o método [ICorProfilerCallback:: JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md) . A enumeração retornada inclui valores para o `COR_PRF_FUNCTION::reJitId` campo. O método [ICorProfilerInfo3:: EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md) , que esse método substitui, não enumera IDs de compilação JIT recompiladas, porque o `COR_PRF_FUNCTION::reJitId` campo é sempre definido como 0. O `ICorProfilerInfo4::EnumJITedFunctions` método enumera as IDs recompiladas do JIT, porque o `COR_PRF_FUNCTION::reJitId` campo está definido corretamente. Observe que o método [ICorProfilerInfo4:: EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md) pode disparar uma coleta de lixo, enquanto o [método ICorProfilerInfo3:: EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md) não fará.  Para obter mais informações, consulte [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md)
- [Interface ICorProfilerInfo4](icorprofilerinfo4-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Criação de perfil](index.md)
