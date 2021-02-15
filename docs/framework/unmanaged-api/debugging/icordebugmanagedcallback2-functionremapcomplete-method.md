---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback2:: FunctionRemapComplete'
title: Método ICorDebugManagedCallback2::FunctionRemapComplete
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.FunctionRemapComplete
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::FunctionRemapComplete
helpviewer_keywords:
- FunctionRemapComplete method [.NET Framework debugging]
- ICorDebugManagedCallback2::FunctionRemapComplete method [.NET Framework debugging]
ms.assetid: 5396c4c3-4ec3-4e3a-a38d-d65b21f0a2fc
topic_type:
- apiref
ms.openlocfilehash: fcb4388185de17d602c1e3dbc725e104a0a48b3b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790836"
---
# <a name="icordebugmanagedcallback2functionremapcomplete-method"></a>Método ICorDebugManagedCallback2::FunctionRemapComplete

Notifica o depurador de que a execução de código mudou para uma nova versão de uma função editada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FunctionRemapComplete (  
    [in] ICorDebugAppDomain   *pAppDomain,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugFunction    *pFunction  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pAppDomain`  
 no Um ponteiro para um objeto ICorDebugAppDomain que representa o domínio do aplicativo que contém a função editada.  
  
 `pThread`  
 no Um ponteiro para um objeto ICorDebugThread que representa o thread no qual o ponto de interrupção do remapeamento foi encontrado.  
  
 `pFunction`  
 no Um ponteiro para um objeto ICorDebugFunction que representa a versão da função em execução no momento no thread.  
  
## <a name="remarks"></a>Comentários  

 Esse retorno de chamada dá ao depurador uma oportunidade de recriar todos os apresentadores que existiam anteriormente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)
- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
