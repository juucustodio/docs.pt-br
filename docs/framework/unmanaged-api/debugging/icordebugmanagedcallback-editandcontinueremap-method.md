---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback:: EditAndContinueRemap'
title: Método ICorDebugManagedCallback::EditAndContinueRemap
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.EditAndContinueRemap
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::EditAndContinueRemap
helpviewer_keywords:
- EditAndContinueRemap method [.NET Framework debugging]
- ICorDebugManagedCallback::EditAndContinueRemap method [.NET Framework debugging]
ms.assetid: 24a8fcce-317e-48ff-aefc-d86123ada935
topic_type:
- apiref
ms.openlocfilehash: ad8932e41236cdb8ed213024efb4175292a5d5f7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790992"
---
# <a name="icordebugmanagedcallbackeditandcontinueremap-method"></a>Método ICorDebugManagedCallback::EditAndContinueRemap

Esse método foi substituído. Ele notifica o depurador de que um evento de remapeamento foi enviado para o ambiente de desenvolvimento integrado (IDE).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EditAndContinueRemap (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugThread *pThread,  
    [in] ICorDebugFunction *pFunction,  
    [in] BOOL fAccurate  
);  
```  
  
## <a name="remarks"></a>Comentários  

 O `EditAndContinueRemap` método é chamado quando a execução do código em uma versão antiga de uma função atualizada foi tentada. O Common Language Runtime chama o `EditAndContinueRemap` método para enviar um evento de remapeamento para o IDE.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
