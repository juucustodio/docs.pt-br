---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ModuleLoadFinished'
title: Método ICorProfilerCallback::ModuleLoadFinished
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ModuleLoadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ModuleLoadFinished
helpviewer_keywords:
- ModuleLoadFinished method [.NET Framework profiling]
- ICorProfilerCallback::ModuleLoadFinished method [.NET Framework profiling]
ms.assetid: 050649e5-ffc0-4458-a0a4-d9ee128a219e
topic_type:
- apiref
ms.openlocfilehash: 960eb9edd036055069ef3f9ab3a93602ce4ef9bf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745340"
---
# <a name="icorprofilercallbackmoduleloadfinished-method"></a>Método ICorProfilerCallback::ModuleLoadFinished

Notifica o criador de perfil que concluiu o carregamento de um módulo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ModuleLoadFinished(  
    [in] ModuleID moduleId,  
    [in] HRESULT  hrStatus);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `moduleId`  
 no A ID do módulo que concluiu o carregamento.  
  
 `hrStatus`  
 no Um HRESULT que indica se o módulo foi carregado com êxito.  
  
## <a name="remarks"></a>Comentários  

 O valor de `moduleId` não é válido para uma solicitação de informações até que o `ModuleLoadFinished` método seja chamado.  
  
 Algumas partes do carregamento do módulo podem continuar após o `ModuleLoadFinished` retorno de chamada. Um HRESULT de falha em `hrStatus` indica uma falha. No entanto, um HRESULT de êxito em `hrStatus` indica apenas que a primeira parte do carregamento do módulo foi bem-sucedida.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método ModuleLoadStarted](icorprofilercallback-moduleloadstarted-method.md)
