---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback:: CreateProcess'
title: Método ICorDebugManagedCallback::CreateProcess
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.CreateProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::CreateProcess
helpviewer_keywords:
- ICorDebugManagedCallback::CreateProcess method [.NET Framework debugging]
- CreateProcess method, ICorDebugManagedCallback interface [.NET Framework debugging]
ms.assetid: 8e89d5ee-e4e3-4738-8302-0b7d1cf4846e
topic_type:
- apiref
ms.openlocfilehash: 564c9862dd90431f0626204fdfe49e59b85a124d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791043"
---
# <a name="icordebugmanagedcallbackcreateprocess-method"></a>Método ICorDebugManagedCallback::CreateProcess

Notifica o depurador quando um processo foi anexado ou iniciado pela primeira vez.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateProcess (  
    [in] ICorDebugProcess *pProcess  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pProcess`  
 no Um ponteiro para um objeto ICorDebugProcess que representa o processo que foi anexado ou iniciado.  
  
## <a name="remarks"></a>Comentários  

 Esse método não é chamado até que o Common Language Runtime seja inicializado. A maioria dos métodos [ICorDebug](icordebug-interface.md) retornará CORDBG_E_NOTREADY antes do `CreateProcess` retorno de chamada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
