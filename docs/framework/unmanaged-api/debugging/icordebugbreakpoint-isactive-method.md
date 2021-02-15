---
description: 'Saiba mais sobre: método ICorDebugBreakpoint:: IsActive'
title: Método ICorDebugBreakpoint::IsActive
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpoint.IsActive
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpoint::IsActive
helpviewer_keywords:
- ICorDebugBreakpoint::IsActive method [.NET Framework debugging]
- IsActive method, ICorDebugBreakpoint interface [.NET Framework debugging]
ms.assetid: 06e583d6-d88a-4ff5-bb95-5c48618a461c
topic_type:
- apiref
ms.openlocfilehash: 49e98ccc3722c37b3ff5968215ef3f658601ea10
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99711785"
---
# <a name="icordebugbreakpointisactive-method"></a>Método ICorDebugBreakpoint::IsActive

Obtém um valor que indica se ele `ICorDebugBreakpoint` está ativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsActive (  
    [out] BOOL *pbActive  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbActive`  
 [fora] `true` Se esse ponto de interrupção estiver ativo; caso contrário, `false` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
