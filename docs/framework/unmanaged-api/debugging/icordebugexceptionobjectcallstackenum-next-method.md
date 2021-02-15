---
description: 'Saiba mais sobre: ICorDebugExceptionObjectCallStackEnum:: Next Method'
title: Método ICorDebugExceptionObjectCallStackEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugExceptionObjectCallStackEnum::Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugExceptionObjectCallStackEnum::Next
helpviewer_keywords:
- ICorDebugExceptionObjectCallStackEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugExceptionObjectCallStackEnum interface [.NET Framework debugging]
ms.assetid: 3328a2c0-1e48-4a54-802a-9b474cf82c21
topic_type:
- apiref
ms.openlocfilehash: df68eb6e4794d294fc39dd943065582dc52a58a1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99693311"
---
# <a name="icordebugexceptionobjectcallstackenumnext-method"></a>Método ICorDebugExceptionObjectCallStackEnum::Next

Obtém o número especificado de instâncias [CorDebugExceptionObjectStackFrame](cordebugexceptionobjectstackframe-structure.md) que contêm informações de uma pilha de chamadas do objeto de exceção.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next(  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)] CorDebugExceptionObjectStackFrame values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 no O número de instâncias de [CorDebugExceptionObjectStackFrame](cordebugexceptionobjectstackframe-structure.md) a serem recuperadas.  
  
 `values`  
 fora Uma matriz de ponteiros, cada um dos quais aponta para um objeto [CorDebugExceptionObjectStackFrame](cordebugexceptionobjectstackframe-structure.md) .  
  
 `pceltFetched`  
 fora Um ponteiro para o número de instâncias de [CorDebugExceptionObjectStackFrame](cordebugexceptionobjectstackframe-structure.md) retornadas na verdade.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
