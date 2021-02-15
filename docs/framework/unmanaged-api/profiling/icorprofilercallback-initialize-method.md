---
description: 'Saiba mais sobre: método ICorProfilerCallback:: Initialize'
title: Método ICorProfilerCallback::Initialize
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.Initialize
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::Initialize
helpviewer_keywords:
- Initialize method, ICorProfilerCallback interface [.NET Framework profiling]
- ICorProfilerCallback::Initialize method [.NET Framework profiling]
ms.assetid: dc5fab2a-4b45-4b12-8727-b89c9915f23e
topic_type:
- apiref
ms.openlocfilehash: b3ff579dee384b331450aa54aace39890febfe30
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99705935"
---
# <a name="icorprofilercallbackinitialize-method"></a>Método ICorProfilerCallback::Initialize

Chamado para inicializar o criador de perfil de código sempre que um novo aplicativo Common Language Runtime (CLR) é iniciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Initialize(  
    [in] IUnknown     *pICorProfilerInfoUnk);  
```  
  
## <a name="parameters"></a>Parâmetros

- `pICorProfilerInfoUnk`

  \[in] ponteiro para uma interface [IUnknown](/cpp/atl/iunknown) que o criador de perfil deve consultar para um ponteiro de interface [ICorProfilerInfo](icorprofilerinfo-interface.md) .  

## <a name="remarks"></a>Comentários  

 A `Initialize` chamada é a única oportunidade para habilitar (ou desabilitar) retornos de chamada que são imutáveis. Depois que um retorno de chamada é habilitado pelo `Initialize` Call, ele não pode ser desabilitado posteriormente usando [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md). O valor COR_PRF_MONITOR_IMMUTABLE da enumeração [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) indica quais eventos são imutáveis.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método Shutdown](icorprofilercallback-shutdown-method.md)
