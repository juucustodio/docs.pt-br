---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ClassLoadStarted'
title: Método ICorProfilerCallback::ClassLoadStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ClassLoadStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ClassLoadStarted
helpviewer_keywords:
- ICorProfilerCallback::ClassLoadStarted method [.NET Framework profiling]
- ClassLoadStarted method [.NET Framework profiling]
ms.assetid: 9f728de8-45c2-45a5-ac4a-45660bd36ecf
topic_type:
- apiref
ms.openlocfilehash: 2474f8041b0858cbcb81d3f4042f1748cb99df3e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99706426"
---
# <a name="icorprofilercallbackclassloadstarted-method"></a>Método ICorProfilerCallback::ClassLoadStarted

Notifica o criador de perfil de que uma classe está sendo carregada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ClassLoadStarted(  
    [in] ClassID classId);  
```  
  
## <a name="parameters"></a>Parâmetros

- `classId`

  \[in] identifica a classe que está sendo carregada.

## <a name="remarks"></a>Comentários  

 O valor de `classId` não é válido para uma solicitação de informações até que o método [ICorProfilerCallback:: ClassLoadFinished](icorprofilercallback-classloadfinished-method.md) seja chamado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
