---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: AssemblyUnloadFinished'
title: Método ICorProfilerCallback::AssemblyUnloadFinished
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AssemblyUnloadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AssemblyUnloadFinished
helpviewer_keywords:
- AssemblyUnloadFinished method [.NET Framework profiling]
- ICorProfilerCallback::AssemblyUnloadFinished method [.NET Framework profiling]
ms.assetid: 53fca564-84b1-44d4-9e21-17a492d2aae7
topic_type:
- apiref
ms.openlocfilehash: 30d6bd805a1466d6a65728b22f677ba00e09ffb6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647996"
---
# <a name="icorprofilercallbackassemblyunloadfinished-method"></a>Método ICorProfilerCallback::AssemblyUnloadFinished

Notifica o criador de perfil de que um assembly foi descarregado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AssemblyUnloadFinished(  
    [in] AssemblyID assemblyId,  
    [in] HRESULT    hrStatus);  
```  
  
## <a name="parameters"></a>Parâmetros

- `assemblyId`

  \[in] identifica o assembly que está sendo descarregado.

- `hrStatus`

  \[in] um HRESULT que indica se o assembly foi descarregado com êxito.

## <a name="remarks"></a>Comentários  

 O valor de `assemblyId` não é válido para uma solicitação de informações depois que o método [ICorProfilerCallback:: AssemblyUnloadStarted](icorprofilercallback-assemblyunloadstarted-method.md) retorna.  
  
 Algumas partes do descarregamento do assembly podem continuar após o `AssemblyUnloadFinished` retorno de chamada. Um HRESULT de falha em `hrStatus` indica uma falha. No entanto, um HRESULT de êxito em `hrStatus` indica apenas que a primeira parte do descarregamento do assembly foi bem-sucedida.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
