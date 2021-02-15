---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: GetFunctionFromToken'
title: Método ICorProfilerInfo::GetFunctionFromToken
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetFunctionFromToken
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetFunctionFromToken
helpviewer_keywords:
- ICorProfilerInfo::GetFunctionFromToken method [.NET Framework profiling]
- GetFunctionFromToken method, ICorProfilerInfo interface [.NET Framework profiling]
ms.assetid: 0eed759f-cce8-405d-88dc-9ee293a38928
topic_type:
- apiref
ms.openlocfilehash: 58dea413539d6e3a625f515aa7e8d5123152c90a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647447"
---
# <a name="icorprofilerinfogetfunctionfromtoken-method"></a>Método ICorProfilerInfo::GetFunctionFromToken

Obtém a ID de uma função. Esse método é obsoleto no .NET Framework versão 2,0. Em vez disso, use o método [ICorProfilerInfo2:: GetFunctionFromTokenAndTypeArgs](icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFunctionFromToken(  
    [in]  ModuleID   moduleId,  
    [in]  mdToken    token,  
    [out] FunctionID *pFunctionId);  
```  
  
## <a name="remarks"></a>Comentários  

 O `GetFunctionFromToken` método não funcionará para funções genéricas ou funções em tipos genéricos; agora é obsoleto. Use `ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs` para todas as funções.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 1,1, 1,0  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
