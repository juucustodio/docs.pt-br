---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: AppDomainShutdownStarted'
title: Método ICorProfilerCallback::AppDomainShutdownStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AppDomainShutdownStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AppDomainShutdownStarted
helpviewer_keywords:
- AppDomainShutdownStarted method [.NET Framework profiling]
- ICorProfilerCallback::AppDomainShutdownStarted method [.NET Framework profiling]
ms.assetid: d23a3408-b525-4aec-a186-2ac7ca65d7a4
topic_type:
- apiref
ms.openlocfilehash: 16545142a512ca1c5f4167f61b81ea949e3d14e4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99648110"
---
# <a name="icorprofilercallbackappdomainshutdownstarted-method"></a>Método ICorProfilerCallback::AppDomainShutdownStarted

Notifica o criador de perfil de que um domínio de aplicativo está sendo descarregado de um processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AppDomainShutdownStarted(  
    [in] AppDomainID appDomainId);  
```  
  
## <a name="parameters"></a>Parâmetros

- `appDomainId`

  \[in] identifica o domínio no qual os assemblies do aplicativo são armazenados.

## <a name="remarks"></a>Comentários  

 O valor de `appDomainId` não é válido para nenhuma solicitação de informações após o `AppDomainShutdownStarted` retorno do método — essa é a última chance do criador de perfil obter informações sobre esse domínio de aplicativo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
