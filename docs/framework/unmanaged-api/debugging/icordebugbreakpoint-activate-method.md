---
description: 'Saiba mais sobre o método: ICorDebugBreakpoint:: Activate'
title: Método ICorDebugBreakpoint::Activate
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpoint.Activate
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpoint::Activate
helpviewer_keywords:
- ICorDebugBreakpoint::Activate method [.NET Framework debugging]
- Activate method [.NET Framework debugging]
ms.assetid: e30c29f7-3f19-4081-b572-a731aa14cd44
topic_type:
- apiref
ms.openlocfilehash: 1a3613ae071b3fc6c4f1005eafd515946d6b2685
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99711838"
---
# <a name="icordebugbreakpointactivate-method"></a>Método ICorDebugBreakpoint::Activate

Define o estado ativo deste `ICorDebugBreakpoint` .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Activate (  
    [in] BOOL bActive  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `bActive`  
 no Defina esse valor como `true` para especificar o estado como ativo; caso contrário, defina esse valor como `false` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
