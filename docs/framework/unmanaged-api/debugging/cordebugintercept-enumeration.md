---
description: 'Saiba mais sobre: enumeração CorDebugIntercept'
title: Enumeração CorDebugIntercept
ms.date: 03/30/2017
api_name:
- CorDebugIntercept
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugIntercept
helpviewer_keywords:
- CorDebugIntercept enumeration [.NET Framework debugging]
ms.assetid: 3d5b642e-7ef2-428b-a5ae-509c35ed461a
topic_type:
- apiref
ms.openlocfilehash: ddd17aff309396fdcda37c731ff907224ee17db2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661968"
---
# <a name="cordebugintercept-enumeration"></a>Enumeração CorDebugIntercept

Indica os tipos de código que podem ser interceptados (ou seja, percorridos).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugIntercept {  
    INTERCEPT_NONE                = 0x0,  
    INTERCEPT_CLASS_INIT          = 0x01,  
    INTERCEPT_EXCEPTION_FILTER    = 0x02,  
    INTERCEPT_SECURITY            = 0x04,  
    INTERCEPT_CONTEXT_POLICY      = 0x08,  
    INTERCEPT_INTERCEPTION        = 0x10,  
    INTERCEPT_ALL                 = 0xffff  
} CorDebugIntercept;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`INTERCEPT_NONE`|Nenhum código pode ser interceptado.|  
|`INTERCEPT_CLASS_INIT`|Um construtor pode ser interceptado.|  
|`INTERCEPT_EXCEPTION_FILTER`|Um filtro de exceção pode ser interceptado.|  
|`INTERCEPT_SECURITY`|O código que impõe a segurança pode ser interceptado.|  
|`INTERCEPT_CONTEXT_POLICY`|Uma política de contexto pode ser interceptada.|  
|`INTERCEPT_INTERCEPTION`|Não usado.|  
|`INTERCEPT_ALL`|Todo o código pode ser interceptado.|  
  
## <a name="remarks"></a>Comentários  

 Use o método [ICorDebugStepper:: SetInterceptMask](icordebugstepper-setinterceptmask-method.md) para estabelecer os tipos de código que podem ser interceptados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
