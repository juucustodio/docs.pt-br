---
description: 'Saiba mais sobre o método: ICorDebugThread:: GetUserState'
title: Método ICorDebugThread::GetUserState
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetUserState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetUserState
helpviewer_keywords:
- GetUserState method, ICorDebugThread interface [.NET Framework debugging]
- ICorDebugThread::GetUserState method [.NET Framework debugging]
ms.assetid: ae0cfd73-8ead-4d36-9310-dccaac9db0bd
topic_type:
- apiref
ms.openlocfilehash: b63b474525534f9e934954ebe660691db90b8b67
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658861"
---
# <a name="icordebugthreadgetuserstate-method"></a>Método ICorDebugThread::GetUserState

Obtém o estado atual do usuário deste ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetUserState (  
    [out] CorDebugUserState   *pState  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pState`  
 fora Um ponteiro para uma combinação de bits de valor de enumeração CorDebugUserState que descreve o estado atual do usuário desse thread.  
  
## <a name="remarks"></a>Comentários  

 O estado do usuário do thread é o estado do thread quando ele é examinado pelo programa que está sendo depurado. Um thread pode ter vários bits de estado definidos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
