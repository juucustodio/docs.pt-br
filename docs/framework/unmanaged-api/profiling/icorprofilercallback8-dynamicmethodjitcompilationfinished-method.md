---
description: 'Saiba mais sobre: ICorProfilerCallback8: método ynamicMethodJITCompilationFinished de:D'
title: 'ICorProfilerCallback8: método ynamicMethodJITCompilationFinished de:D'
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback8.DynamicMethodJITCompilationFinished
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.openlocfilehash: d076307b9e57c27753297cad8eebc1b9aa9433f6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781708"
---
# <a name="icorprofilercallback8dynamicmethodjitcompilationfinished-method"></a>ICorProfilerCallback8: método ynamicMethodJITCompilationFinished de:D

[Com suporte no .NET Framework 4,7 e versões posteriores]  
  
Notifica o criador de perfil sempre que a compilação JIT de um método dinâmico for concluída.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DynamicMethodJITCompilationFinished(  
     [in]  FunctionID  functionId,
     [in]  BOOL        hrStatus,
     [in]  BOOL        fIsSafeToBlock
);  
```  
  
## <a name="parameters"></a>Parâmetros  

[in] `functionId`  
O identificador da função na memória para a qual a compilação JIT é iniciada.

[in] `hrStatus` Um valor que indica se a compilação JIT foi bem-sucedida.

[in] `fIsSafeToBlock` 
 `true` para indicar que o bloqueio pode fazer com que o tempo de execução aguarde o thread de chamada retornar desse retorno de chamada; `false`para indicar que o bloqueio não afetará a operação do tempo de execução.  

## <a name="remarks"></a>Comentários  

Esse retorno de chamada é disparado sempre que a compilação JIT de um método dinâmico é concluída. Isso inclui vários stubs IL e métodos LCG. Seu objetivo é fornecer aos gravadores de criador de perfil informações suficientes para identificar o método compilado para os usuários.

> [!NOTE]
> `functionId` os valores não podem ser usados para resolver seus tokens de metadados, pois os métodos dinâmicos não têm metadados.

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método DynamicMethodJITCompilationStarted](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)
- [Interface ICorProfilerCallback8](icorprofilercallback8-interface.md)
