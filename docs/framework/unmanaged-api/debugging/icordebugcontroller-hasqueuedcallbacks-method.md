---
description: 'Saiba mais sobre o método: ICorDebugController:: HasQueuedCallbacks'
title: Método ICorDebugController::HasQueuedCallbacks
ms.date: 03/30/2017
api_name:
- ICorDebugController.HasQueuedCallbacks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::HasQueuedCallbacks
helpviewer_keywords:
- HasQueuedCallbacks method [.NET Framework debugging]
- ICorDebugController::HasQueuedCallbacks method [.NET Framework debugging]
ms.assetid: 0d6a1cd9-370b-4462-adbf-e3980e897ea7
topic_type:
- apiref
ms.openlocfilehash: bdc22831b912d3bad565b6abf5c73591d07ffe11
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764627"
---
# <a name="icordebugcontrollerhasqueuedcallbacks-method"></a>Método ICorDebugController::HasQueuedCallbacks

Obtém um valor que indica se qualquer retorno de chamada gerenciado está na fila no momento para o thread especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT HasQueuedCallbacks (  
    [in] ICorDebugThread *pThread,  
    [out] BOOL           *pbQueued  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pThread`  
 no Um ponteiro para um objeto "ICorDebugThread" que representa o thread.  
  
 `pbQueued`  
 fora Um ponteiro para um valor que ocorrerá `true` se qualquer retorno de chamada gerenciado estiver na fila no momento para o thread especificado; caso contrário, `false` .  
  
 Se NULL for especificado para o `pThread` parâmetro, `HasQueuedCallbacks` retornará `true` se houver retornos de chamada atualmente gerenciados em fila para qualquer thread.  
  
## <a name="remarks"></a>Comentários  

 Os retornos de chamada serão expedidos um de cada vez, sempre que [ICorDebugController:: Continue](icordebugcontroller-continue-method.md) for chamado. O depurador pode verificar esse sinalizador se desejar relatar vários eventos de depuração que ocorrem simultaneamente.  
  
 Quando os eventos de depuração são enfileirados, eles já ocorreram, portanto, o depurador deve drenar toda a fila para ter certeza do estado do depurado. (Chamada `ICorDebugController::Continue` para drenar a fila.) Por exemplo, se a fila contiver dois eventos de depuração no thread *x* e o depurador suspender o thread *x* após o primeiro evento de depuração e, em seguida `ICorDebugController::Continue` , chamar, o segundo evento de depuração para o thread *x* será expedido, embora o thread tenha sido suspenso.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Confira também
