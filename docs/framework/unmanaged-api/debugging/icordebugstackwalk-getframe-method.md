---
description: 'Saiba mais sobre: método ICorDebugStackWalk:: GetFrame'
title: Método ICorDebugStackWalk::GetFrame
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk.GetFrame Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk::GetFrame
helpviewer_keywords:
- GetFrame method [.NET Framework debugging]
- ICorDebugStackWalk::GetFrame method [.NET Framework debugging]
ms.assetid: 4083b505-5b59-44fb-8c5d-129db6a96c10
topic_type:
- apiref
ms.openlocfilehash: b00ddb6a475aff4263a922f5a20b866cd0e1b2ed
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794735"
---
# <a name="icordebugstackwalkgetframe-method"></a>Método ICorDebugStackWalk::GetFrame

Obtém o quadro atual no objeto [ICorDebugStackWalk](icordebugstackwalk-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFrame([out] ICorDebugFrame ** pFrame);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pFrame`  
 no Um ponteiro para o endereço do objeto frame criado que representa o quadro atual na pilha.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O tempo de execução retornou com êxito o quadro atual.|  
|E_FAIL|O quadro atual não foi retornado.|  
|S_FALSE|O quadro atual é um quadro de ativação nativo.|  
|E_INVALIDARG|`pFrame` é nulo.|  
|CORDBG_E_PAST_END_OF_STACK|O ponteiro de quadro já está no final da pilha; Portanto, nenhum quadro adicional pode ser acessado.|  
  
## <a name="exceptions"></a>Exceções  
  
## <a name="remarks"></a>Comentários  

 `ICorDebugStackWalk` retorna apenas os quadros de pilhas reais. Use o método [ICorDebugThread3:: GetActiveInternalFrames](icordebugthread3-getactiveinternalframes-method.md) para retornar quadros internos. (Os quadros internos são estruturas de dados enviadas por push para a pilha pelo tempo de execução para armazenar dados temporários.)  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugStackWalk](icordebugstackwalk-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
