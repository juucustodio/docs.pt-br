---
description: 'Saiba mais sobre: Enumeração CorDebugInternalFrameType'
title: Enumeração CorDebugInternalFrameType
ms.date: 03/30/2017
api_name:
- CorDebugInternalFrameType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugInternalFrameType
helpviewer_keywords:
- CorDebugInternalFrameType enumeration [.NET Framework debugging]
ms.assetid: e4412dc2-c338-4cfb-94d8-f682095dd2b1
topic_type:
- apiref
ms.openlocfilehash: 0479ae7602224e03086b9dacf91d360253b61818
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661981"
---
# <a name="cordebuginternalframetype-enumeration"></a>Enumeração CorDebugInternalFrameType

Identifica o tipo de quadro de pilha. Essa enumeração é usada pelo método [ICorDebugInternalFrame:: GetFrameType](icordebuginternalframe-getframetype-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugInternalFrameType {  
  
    STUBFRAME_NONE                 = 0x00000000,  
    STUBFRAME_M2U                  = 0x00000001,  
    STUBFRAME_U2M                  = 0x00000002,  
    STUBFRAME_APPDOMAIN_TRANSITION = 0x00000003,  
    STUBFRAME_LIGHTWEIGHT_FUNCTION = 0x00000004,  
    STUBFRAME_FUNC_EVAL            = 0x00000005,  
    STUBFRAME_INTERNALCALL         = 0x00000006,  
    STUBFRAME_CLASS_INIT           = 0x00000007,  
    STUBFRAME_EXCEPTION            = 0x00000008,  
    STUBFRAME_SECURITY             = 0x00000009,  
    STUBFRAME_JIT_COMPILATION     = 0x0000000a,  
} CorDebugInternalFrameType;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`STUBFRAME_NONE`|Um valor nulo. O `ICorDebugInternalFrame::GetFrameType` método nunca retorna esse valor.|  
|`STUBFRAME_M2U`|Um quadro de stub gerenciado para não gerenciado.|  
|`STUBFRAME_U2M`|Um quadro de stub não gerenciado para gerenciamento.|  
|`STUBFRAME_APPDOMAIN_TRANSITION`|Uma transição entre domínios de aplicativo.|  
|`STUBFRAME_LIGHTWEIGHT_FUNCTION`|Uma chamada de método leve.|  
|`STUBFRAME_FUNC_EVAL`|O início da avaliação da função.|  
|`STUBFRAME_INTERNALCALL`|Uma chamada interna para o Common Language Runtime.|  
|`STUBFRAME_CLASS_INIT`|O início de uma inicialização de classe.|  
|`STUBFRAME_EXCEPTION`|Uma exceção que é lançada.|  
|`STUBFRAME_SECURITY`|Um quadro usado para segurança de acesso ao código.|  
|`STUBFRAME_JIT_COMPILATION`|O tempo de execução é a compilação JIT de um método.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
