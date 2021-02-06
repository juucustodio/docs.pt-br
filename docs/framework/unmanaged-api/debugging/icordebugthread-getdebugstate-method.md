---
description: 'Saiba mais sobre o método: ICorDebugThread:: getdebugstate'
title: Método ICorDebugThread::GetDebugState
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetDebugState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetDebugState
helpviewer_keywords:
- GetDebugState method [.NET Framework debugging]
- ICorDebugThread::GetDebugState method [.NET Framework debugging]
ms.assetid: 9be27b0c-1d99-4722-b0d4-40cf6753ce5c
topic_type:
- apiref
ms.openlocfilehash: 86534dded9b8e931fe2a7e44f1c95dc2ec7b6f0d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659147"
---
# <a name="icordebugthreadgetdebugstate-method"></a>Método ICorDebugThread::GetDebugState

Obtém o estado de depuração atual deste objeto ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDebugState (  
    [out] CorDebugThreadState   *pState  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pState`  
 fora Um ponteiro para uma combinação de bits de valor de enumeração CorDebugThreadState que descreve o estado de depuração atual desse thread.  
  
## <a name="remarks"></a>Comentários  

 Se o processo estiver parado no momento, `pState` representará o estado de depuração que existiria para esse thread se o processo fosse continuado, não o estado real atual desse thread.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
