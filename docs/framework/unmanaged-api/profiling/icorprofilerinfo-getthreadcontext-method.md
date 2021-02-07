---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: GetThreadContext'
title: Método ICorProfilerInfo::GetThreadContext
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetThreadContext
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetThreadContext
helpviewer_keywords:
- ICorProfilerInfo::GetThreadContext method [.NET Framework profiling]
- GetThreadContext method, ICorProfilerInfo interface [.NET Framework profiling]
ms.assetid: 79446216-4b8b-484c-8fe3-e87dbf9df2fd
topic_type:
- apiref
ms.openlocfilehash: b2970da90250819cc68eee55b70188d4830113a6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99687266"
---
# <a name="icorprofilerinfogetthreadcontext-method"></a>Método ICorProfilerInfo::GetThreadContext

Obtém a identidade de contexto atualmente associada ao thread especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetThreadContext(  
    [in]  ThreadID  threadId,  
    [out] ContextID *pContextId);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `threadId`  
 no A ID do thread.  
  
 `pContextId`  
 fora Um ponteiro para a ID de contexto atualmente associada ao thread especificado. Se o thread não tiver nenhum contexto associado a ele no momento, essa função retornará CORPROF_E_DATAINCOMPLETE.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
