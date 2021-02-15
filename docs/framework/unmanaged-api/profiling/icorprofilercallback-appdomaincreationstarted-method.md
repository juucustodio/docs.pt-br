---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: AppDomainCreationStarted'
title: Método ICorProfilerCallback::AppDomainCreationStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AppDomainCreationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AppDomainCreationStarted
helpviewer_keywords:
- AppDomainCreationStarted method [.NET Framework profiling]
- ICorProfilerCallback::AppDomainCreationStarted method [.NET Framework profiling]
ms.assetid: b2a8240b-07fe-4859-bb2b-7d3adbfa0a9f
topic_type:
- apiref
ms.openlocfilehash: 00ebbe35f6f4446caeee5ebcd56b853d6e6dc80c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99648220"
---
# <a name="icorprofilercallbackappdomaincreationstarted-method"></a>Método ICorProfilerCallback::AppDomainCreationStarted

Notifica o criador de perfil de que um domínio de aplicativo está sendo criado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AppDomainCreationStarted(  
    [in] AppDomainID appDomainId);  
```  
  
## <a name="parameters"></a>Parâmetros

- `appDomainId`

  \[em] identifica o domínio que está sendo criado.
  
## <a name="remarks"></a>Comentários  

 A ID não é válida para nenhuma solicitação de informação até que o método [ICorProfilerCallback:: AppDomainCreationFinished](icorprofilercallback-appdomaincreationfinished-method.md) seja chamado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
