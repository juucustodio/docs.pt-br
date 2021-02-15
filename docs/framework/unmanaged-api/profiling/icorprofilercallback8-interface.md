---
description: 'Saiba mais sobre: interface ICorProfilerCallback8'
title: Interface ICorProfilerCallback8
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback8
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.openlocfilehash: 8dd9b8eea82f38b7598d578bd718743af826070d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781669"
---
# <a name="icorprofilercallback8-interface"></a>Interface ICorProfilerCallback8

[Com suporte no .NET Framework 4,7 e versões posteriores]  

 Uma subclasse de [ICorProfilerCallback7](icorprofilercallback7-interface.md) que fornece métodos de retorno de chamada usados pelo Common Language Runtime para notificar o criador de perfil de que a compilação JIT de um método dinâmico foi iniciada e concluída.
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método DynamicMethodJITCompilationStarted](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)|Notifica o criador de perfil de que a compilação JIT de um método dinâmico foi iniciada.|  
|[Método DynamicMethodJITCompilationFinished](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)|Notifica o criador de perfil de que a compilação JIT de um método dinâmico foi concluída.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Interface ICorProfilerCallback9](icorprofilercallback9-interface.md)
