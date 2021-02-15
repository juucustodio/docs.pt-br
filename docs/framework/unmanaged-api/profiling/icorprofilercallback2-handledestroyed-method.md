---
description: 'Saiba mais sobre o método: ICorProfilerCallback2:: HandleDestroyed'
title: Método ICorProfilerCallback2::HandleDestroyed
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.HandleDestroyed
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::HandleDestroyed
helpviewer_keywords:
- ICorProfilerCallback2::HandleDestroyed method [.NET Framework profiling]
- HandleDestroyed method [.NET Framework profiling]
ms.assetid: ab4f4bbd-40c7-4667-bfde-60cd73803110
topic_type:
- apiref
ms.openlocfilehash: d583a2170efbb4ebe72d7eacdd60af1a089a518f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99705560"
---
# <a name="icorprofilercallback2handledestroyed-method"></a>Método ICorProfilerCallback2::HandleDestroyed

Notifica o criador de perfil de código de que um identificador de coleta de lixo foi destruído.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT HandleDestroyed(  
    [in] GCHandleID handleId);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `handleId`  
 no A ID do identificador para a coleta de lixo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Interface ICorProfilerCallback2](icorprofilercallback2-interface.md)
