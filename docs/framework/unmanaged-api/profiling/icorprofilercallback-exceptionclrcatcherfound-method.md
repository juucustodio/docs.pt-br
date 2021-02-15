---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ExceptionCLRCatcherFound'
title: Método ICorProfilerCallback::ExceptionCLRCatcherFound
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionCLRCatcherFound
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionCLRCatcherFound
helpviewer_keywords:
- ICorProfilerCallback::ExceptionCLRCatcherFound method [.NET Framework profiling]
- ExceptionCLRCatcherFound method [.NET Framework profiling]
ms.assetid: 73fe8b4b-8f9a-4ba5-a10c-b26521396a66
topic_type:
- apiref
ms.openlocfilehash: 37027a00e488eed5681b1d99ada6332d59e6a632
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99706299"
---
# <a name="icorprofilercallbackexceptionclrcatcherfound-method"></a>Método ICorProfilerCallback::ExceptionCLRCatcherFound

Chamado quando um `catch` bloco de uma exceção é encontrado dentro do Common Language Runtime (CLR) em si. Esse método é obsoleto no .NET Framework versão 2,0.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT ExceptionCLRCatcherFound();  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versão do .NET Framework:** 1,0  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método ExceptionCLRCatcherExecute](icorprofilercallback-exceptionclrcatcherexecute-method.md)
