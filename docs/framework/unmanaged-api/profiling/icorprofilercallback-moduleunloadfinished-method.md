---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ModuleUnloadFinished'
title: Método ICorProfilerCallback::ModuleUnloadFinished
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ModuleUnloadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ModuleUnloadFinished
helpviewer_keywords:
- ModuleUnloadFinished method [.NET Framework profiling]
- ICorProfilerCallback::ModuleUnloadFinished method [.NET Framework profiling]
ms.assetid: 185e3327-9f9c-44bc-8a5c-febea9a6bb5b
topic_type:
- apiref
ms.openlocfilehash: 32182beb879813a4e60f69494bd93799c0f66e1d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745249"
---
# <a name="icorprofilercallbackmoduleunloadfinished-method"></a>Método ICorProfilerCallback::ModuleUnloadFinished

Notifica o criador de perfil de que um módulo concluiu o descarregamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ModuleUnloadFinished(  
    [in] ModuleID moduleId,  
    [in] HRESULT  hrStatus);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `moduleId`  
 no A ID do módulo que foi descarregado.  
  
 `hrStatus`  
 no Um HRESULT que indica se o módulo foi descarregado com êxito.  
  
## <a name="remarks"></a>Comentários  

 O valor de `moduleId` não é válido para uma solicitação de informações depois que o método [ICorProfilerCallback:: ModuleUnloadStarted](icorprofilercallback-moduleunloadstarted-method.md) retorna.  
  
 Algumas partes do descarregamento da classe podem continuar após o `ModuleUnloadFinished` retorno de chamada. Um HRESULT de falha em `hrStatus` indica uma falha. No entanto, um HRESULT de êxito em `hrStatus` indica apenas que a primeira parte do descarregamento do módulo foi bem-sucedida.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
