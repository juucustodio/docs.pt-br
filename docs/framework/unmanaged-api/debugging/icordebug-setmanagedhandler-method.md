---
description: 'Saiba mais sobre o método: ICorDebug:: SetManagedHandler'
title: Método ICorDebug::SetManagedHandler
ms.date: 03/30/2017
api_name:
- ICorDebug.SetManagedHandler
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::SetManagedHandler
helpviewer_keywords:
- ICorDebug::SetManagedHandler method [.NET Framework debugging]
- SetManagedHandler method [.NET Framework debugging]
ms.assetid: d079131b-685b-4869-95be-826b88d28bd2
topic_type:
- apiref
ms.openlocfilehash: 5817bd39a2c4e7c71dc12ca8d2d9b1263d116ac8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754349"
---
# <a name="icordebugsetmanagedhandler-method"></a>Método ICorDebug::SetManagedHandler

Especifica o objeto manipulador de eventos para eventos gerenciados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetManagedHandler (  
    [in] ICorDebugManagedCallback     *pCallback  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pCallback`  
 no Um ponteiro para um objeto [ICorDebugManagedCallback](icordebugmanagedcallback-interface.md) , que é o objeto manipulador de eventos.  
  
## <a name="remarks"></a>Comentários  

 `SetManagedHandler` deve ser chamado no momento da criação.  
  
 Se a `ICorDebugManagedCallback` implementação não contiver interfaces suficientes para lidar com eventos de depuração para o aplicativo que está sendo depurado, `SetManagedHandler` o retornará um HRESULT de E_NOINTERFACE.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebug](icordebug-interface.md)
