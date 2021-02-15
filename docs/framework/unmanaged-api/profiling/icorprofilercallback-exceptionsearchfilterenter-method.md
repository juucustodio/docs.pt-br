---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ExceptionSearchFilterEnter'
title: Método ICorProfilerCallback::ExceptionSearchFilterEnter
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionSearchFilterEnter
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionSearchFilterEnter
helpviewer_keywords:
- ExceptionSearchFilterEnter method [.NET Framework profiling]
- ICorProfilerCallback::ExceptionSearchFilterEnter method [.NET Framework profiling]
ms.assetid: acc239ce-3eef-418c-b1df-c5a6dd8e8a4c
topic_type:
- apiref
ms.openlocfilehash: ca0eb80f57d7c00d0abfab1bb602650c951a30e3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745353"
---
# <a name="icorprofilercallbackexceptionsearchfilterenter-method"></a>Método ICorProfilerCallback::ExceptionSearchFilterEnter

Notifica o criador de perfil de que a fase de pesquisa do tratamento de exceções começou a executar um filtro de exceção definido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ExceptionSearchFilterEnter(  
    [in] FunctionID functionId);  
```  
  
## <a name="parameters"></a>Parâmetros

- `functionId`

  \[in] a ID da função que contém o filtro.

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método ExceptionSearchFilterLeave](icorprofilercallback-exceptionsearchfilterleave-method.md)
