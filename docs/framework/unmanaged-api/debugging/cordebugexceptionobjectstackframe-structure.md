---
description: 'Saiba mais sobre: estrutura CorDebugExceptionObjectStackFrame'
title: Estrutura CorDebugExceptionObjectStackFrame
ms.date: 03/30/2017
api_name:
- CorDebugExceptionObjectStackFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugExceptionObjectStackFrame
helpviewer_keywords:
- CorDebugExceptionObjectStackFrame structure [.NET Framework debugging]
ms.assetid: 542cdd81-5ae7-4361-b0ef-1ae4775df258
topic_type:
- apiref
ms.openlocfilehash: abeb5a9f6385c494745a34c6f37d6fbc1376ad7b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662150"
---
# <a name="cordebugexceptionobjectstackframe-structure"></a>Estrutura CorDebugExceptionObjectStackFrame

Representa informações de quadro de pilha de um objeto de exceção.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct CorDebugExceptionObjectStackFrame {  
    ICorDebugModule* pModule;  
    CORDB_ADDRESS ip;  
    mdMethodDef methodDef;  
    BOOL isLastForeignExceptionFrame;  
} CorDebugExceptionObjectStackFrame;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`pModule`|Um ponteiro para o objeto ICorDebugModule para o quadro atual.|  
|`ip`|O valor do ponteiro de instrução (EIP/RIP) para o quadro atual.|  
|`methodDef`|O token do método para o quadro atual.|  
|`isLastForeignExceptionFrame`|Um valor que indica se o quadro é o último quadro em uma exceção estrangeira.|  
  
## <a name="remarks"></a>Comentários  

 O chamador deve liberar o ponteiro para o objeto ICorDebugModule depois que ele não estiver mais em uso.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
