---
description: 'Saiba mais sobre o método: ICorDebugThread:: GetID'
title: Método ICorDebugThread::GetID
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetID
helpviewer_keywords:
- ICorDebugThread::GetID method [.NET Framework debugging]
- GetID method, ICorDebugThread interface [.NET Framework debugging]
ms.assetid: f1de4584-92df-42f3-9da4-fca03a1c6821
topic_type:
- apiref
ms.openlocfilehash: d089201527da67299b64cdf074bdd331f22375a1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659069"
---
# <a name="icordebugthreadgetid-method"></a>Método ICorDebugThread::GetID

Obtém o identificador do sistema operacional atual da parte ativa deste ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetID (  
    [out] DWORD *pdwThreadId  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pdwThreadId`  
 fora O identificador do thread.  
  
## <a name="remarks"></a>Comentários  

 O identificador do sistema operacional pode potencialmente ser alterado durante a execução de um processo e pode ser um valor diferente para diferentes partes do thread.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
