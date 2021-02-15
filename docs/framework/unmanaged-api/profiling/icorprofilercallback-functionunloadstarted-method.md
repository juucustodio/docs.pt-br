---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: FunctionUnloadStarted'
title: Método ICorProfilerCallback::FunctionUnloadStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.FunctionUnloadStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::FunctionUnloadStarted
helpviewer_keywords:
- FunctionUnloadStarted method [.NET Framework profiling]
- ICorProfilerCallback::FunctionUnloadStarted method [.NET Framework profiling]
ms.assetid: d6a5fa8b-09c6-47a5-b60e-6cf2e355df30
topic_type:
- apiref
ms.openlocfilehash: 3dd5d46a224c0c51dfee251cf5d0c6ae9320b630
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99705948"
---
# <a name="icorprofilercallbackfunctionunloadstarted-method"></a>Método ICorProfilerCallback::FunctionUnloadStarted

Notifica o criador de perfil de que o tempo de execução começou a descarregar uma função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FunctionUnloadStarted(  
    [in] FunctionID functionId);
```  
  
## <a name="parameters"></a>Parâmetros

- `functionId`

  \[in] a ID da função que está sendo descarregada.

## <a name="remarks"></a>Comentários  

 O valor do `functionId` parâmetro não é mais válido depois que esse método retorna ao chamador.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
