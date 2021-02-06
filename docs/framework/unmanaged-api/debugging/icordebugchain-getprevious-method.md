---
description: 'Saiba mais sobre: método ICorDebugChain:: getprevious'
title: Método ICorDebugChain::GetPrevious
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetPrevious
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetPrevious
helpviewer_keywords:
- ICorDebugChain::GetPrevious method [.NET Framework debugging]
- GetPrevious method [.NET Framework debugging]
ms.assetid: 58eed4c8-d80c-4c6a-a875-967a90dd926c
topic_type:
- apiref
ms.openlocfilehash: 169c46afd545835e6da87686a8e74ecd12173904
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661253"
---
# <a name="icordebugchaingetprevious-method"></a>Método ICorDebugChain::GetPrevious

Obtém a cadeia de quadros anterior para o thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetPrevious (  
    [out] ICorDebugChain     **ppChain  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppChain`  
 fora Um ponteiro para o endereço de um objeto ICorDebugChain que representa a cadeia de quadros anterior para esse thread. Se essa cadeia for a primeira cadeia, `ppChain` será NULL.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
