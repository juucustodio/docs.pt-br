---
description: 'Saiba mais sobre: interface ICorProfilerFunctionControl'
title: Interface ICorProfilerFunctionControl
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl
helpviewer_keywords:
- ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: 4e3d3141-4662-4166-8f05-bc857c1b4216
topic_type:
- apiref
ms.openlocfilehash: 7b4ac58d2b8754108b4e10493596776987a93a49
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753309"
---
# <a name="icorprofilerfunctioncontrol-interface"></a>Interface ICorProfilerFunctionControl

Fornece métodos que permitem a um criador de perfis de código se comunicar com o Common Language runtime (CLR) para controlar como o compilador JIT deve gerar código ao recompilar um método específico.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método SetCodegenFlags](icorprofilerfunctioncontrol-setcodegenflags-method.md)|Define um ou mais sinalizadores da enumeração de [COR_PRF_CODEGEN_FLAGS](cor-prf-codegen-flags-enumeration.md) para controlar a geração de código para uma função recompilada JIT (just-in-time).|  
|[Método SetILFunctionBody](icorprofilerfunctioncontrol-setilfunctionbody-method.md)|Substitui o corpo CIL (Common Intermediate Language) do método.|  
|[Método SetILInstrumentedCodeMap](icorprofilerfunctioncontrol-setilinstrumentedcodemap-method.md)|Define um mapa de códigos para a função especificada usando as entradas de mapa Common Intermediate Language (CIL) especificadas.|  
  
## <a name="remarks"></a>Comentários  

 A interface de `ICorProfilerFunctionControl` fornece métodos para controlar a geração de código para uma única função recompilada. O criador de perfil Obtém uma instância dessa interface por meio do retorno de chamada [ICorProfilerCallback4:: GetReJITParameters](icorprofilercallback4-getrejitparameters-method.md) . Cada instância do `ICorProfilerFunctionControl` controla todas as instâncias de uma função.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo4](icorprofilerinfo4-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Método EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md)
