---
description: 'Saiba mais sobre o método: ICorDebugExceptionDebugEvent:: GetNativeIP'
title: 'Método ICorDebugExceptionDebugEvent:: GetNativeIP'
ms.date: 03/30/2017
ms.assetid: 12e6a262-d9ac-49b8-9b80-1e653a2a3819
ms.openlocfilehash: 89bda36efc59e2462634c3d8a3a5835c9d4b3354
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99693454"
---
# <a name="icordebugexceptiondebugeventgetnativeip-method"></a>Método ICorDebugExceptionDebugEvent:: GetNativeIP

Obtém o ponteiro de instrução nativa para este evento de depuração de exceção.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetNativeIP(  
   [out]CORDB_ADDRESS *pIP  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pIP`  
 fora Um ponteiro para o ponteiro de instrução deste evento de depuração de exceção. Consulte a seção Comentários para obter mais informações.  
  
## <a name="remarks"></a>Comentários  

 O significado desse ponteiro de instrução depende do tipo de evento, conforme mostrado na tabela a seguir.  
  
|Tipo de evento|Significado do `pStackPointer` valor|  
|----------------|--------------------------------------|  
|[MANAGED_EXCEPTION_FIRST_CHANCE](cordebugrecordformat-enumeration.md)|O endereço da instrução com falha.|  
|[MANAGED_EXCEPTION_USER_FIRST_CHANCE](cordebugrecordformat-enumeration.md)|O endereço do código no quadro indicado pelo método [GetStackPointer](icordebugexceptiondebugevent-getstackpointer-method.md) em que a execução será retomada se nenhuma exceção tivesse sido gerada. A exceção pode ou não causar código diferente, como o bloco catch de uma `try/catch/finally` cláusula, a ser executado nesse quadro.|  
|[MANAGED_EXCEPTION_CATCH_HANDLER_FOUND](cordebugrecordformat-enumeration.md)|O endereço de código onde a `catch` execução do manipulador será iniciada no quadro indicado pelo método [GetStackPointer](icordebugexceptiondebugevent-getstackpointer-method.md) .|  
|[MANAGED_EXCEPTION_UNHANDLED](cordebugrecordformat-enumeration.md)|`pIP` é 0.|  
  
 O tipo de evento está disponível no método [ICorDebugDebugEvent:: GetEventKind](icordebugdebugevent-geteventkind-method.md) .  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugExceptionDebugEvent](icordebugexceptiondebugevent-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
