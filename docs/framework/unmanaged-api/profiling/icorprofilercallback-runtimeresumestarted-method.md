---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: RuntimeResumeStarted'
title: Método ICorProfilerCallback::RuntimeResumeStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RuntimeResumeStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RuntimeResumeStarted
helpviewer_keywords:
- ICorProfilerCallback::RuntimeResumeStarted method [.NET Framework profiling]
- RuntimeResumeStarted method [.NET Framework profiling]
ms.assetid: 5854bfb2-c568-4f19-904a-7c9d41e7b995
topic_type:
- apiref
ms.openlocfilehash: 74e87906b4c429d795aa3074b25f4ac7a9edfa37
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99788833"
---
# <a name="icorprofilercallbackruntimeresumestarted-method"></a>Método ICorProfilerCallback::RuntimeResumeStarted

Notifica o criador de perfil de que o tempo de execução está retomando todos os threads em tempo de execução.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT RuntimeResumeStarted();  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método RuntimeResumeFinished](icorprofilercallback-runtimeresumefinished-method.md)
