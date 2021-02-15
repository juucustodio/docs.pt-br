---
description: 'Saiba mais sobre: ICorDebugBreakpointEnum:: Next Method'
title: Método ICorDebugBreakpointEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpointEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpointEnum::Next
helpviewer_keywords:
- Next method, ICorDebugBreakpointEnum interface [.NET Framework debugging]
- ICorDebugBreakpointEnum::Next method [.NET Framework debugging]
ms.assetid: 2e6bbaea-79ba-448c-a0e3-7c90fc7c2939
topic_type:
- apiref
ms.openlocfilehash: 966494bbabaca99b6b5168db6fb7616c15c537e1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99711668"
---
# <a name="icordebugbreakpointenumnext-method"></a>Método ICorDebugBreakpointEnum::Next

Obtém o número especificado de instâncias de ICorDebugBreakpoint da enumeração, começando na posição atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next (  
    [in] ULONG  celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugBreakpoint *breakpoints[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 no O número de `ICorDebugBreakpoint` instâncias a serem recuperadas.  
  
 `breakpoints`  
 fora Uma matriz de ponteiros, cada um dos quais aponta para um `ICorDebugBreakpoint` objeto que representa um ponto de interrupção.  
  
 `pceltFetched`  
 fora Um ponteiro para o número de `ICorDebugBreakpoint` instâncias retornadas de fato. Esse valor pode ser nulo se `celt` for um.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
