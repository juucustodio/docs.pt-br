---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: GetThreadInfo'
title: Método ICorProfilerInfo::GetThreadInfo
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetThreadInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetThreadInfo
helpviewer_keywords:
- ICorProfilerInfo::GetThreadInfo method [.NET Framework profiling]
- GetThreadInfo method [.NET Framework profiling]
ms.assetid: fc994fef-65c9-432a-84cb-66c8141147e7
topic_type:
- apiref
ms.openlocfilehash: 5514b1c4860067a07bf922e9d9a8bfab8c05e218
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760544"
---
# <a name="icorprofilerinfogetthreadinfo-method"></a>Método ICorProfilerInfo::GetThreadInfo

Obtém a identidade do Thread Win32 atual para o thread especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetThreadInfo(  
    [in]  ThreadID threadId,  
    [out] DWORD    *pdwWin32ThreadId);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `threadId`  
 no A ID do thread para o qual obter a ID do Win32 atual.  
  
 `pdwWin32ThreadId`  
 fora Um ponteiro para a ID de thread do Win32 atual do thread especificado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
