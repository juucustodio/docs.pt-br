---
description: 'Saiba mais sobre: interface ICorProfilerCallback9'
title: Interface ICorProfilerCallback9
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback9
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.openlocfilehash: 4bfcaf6f8985909ef9142ef4d08535a19facd7e7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781643"
---
# <a name="icorprofilercallback9-interface"></a>Interface ICorProfilerCallback9

[Com suporte no .NET Framework 4.7.2 e versões posteriores]  

 Uma subclasse de [ICorProfilerCallback8](icorprofilercallback8-interface.md) que fornece um método de retorno de chamada usado pelo Common Language Runtime para notificar o criador de perfil de que um método dinâmico tem sido coletado como lixo e subsequentemente descarregado.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método DynamicMethodUnloaded](ICorProfilerCallback9-dynamicmethodunloaded-method.md)|Notifica o criador de perfil de que um método dinâmico foi coletado como lixo e subsequentemente descarregado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
**.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  

## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Interface ICorProfilerCallback8](icorprofilercallback9-interface.md)
- [Método ICorProfilerCallback8. DynamicMethodJITCompilationStarted](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)
- [Método ICorProfilerCallback8. DynamicMethodJITCompilationFinished](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)
