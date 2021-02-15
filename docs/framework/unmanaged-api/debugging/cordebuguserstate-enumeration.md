---
description: 'Saiba mais sobre: Enumeração CorDebugUserState'
title: Enumeração CorDebugUserState
ms.date: 03/30/2017
api_name:
- CorDebugUserState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugUserState
helpviewer_keywords:
- CorDebugUserState enumeration [.NET Framework debugging]
ms.assetid: 5f6c2bcd-8102-4e3b-abc5-86ab0bd62def
topic_type:
- apiref
ms.openlocfilehash: c556e7943751fb8e159e3e0d0b9a71baf1f6b5b5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661734"
---
# <a name="cordebuguserstate-enumeration"></a>Enumeração CorDebugUserState

Indica o estado do usuário de um thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugUserState {  
    USER_STOP_REQUESTED     =  0x01,  
    USER_SUSPEND_REQUESTED  =  0x02,  
    USER_BACKGROUND         =  0x04,  
    USER_UNSTARTED          =  0x08,  
    USER_STOPPED            =  0x10,  
    USER_WAIT_SLEEP_JOIN    =  0x20,  
    USER_SUSPENDED          =  0x40,  
    USER_UNSAFE_POINT       =  0x80,  
    USER_THREADPOOL         = 0x100  
} CorDebugUserState;  
```  
  
## <a name="members"></a>Membros  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`USER_STOP_REQUESTED`|Foi solicitada uma terminação do thread.|  
|`USER_SUSPEND_REQUESTED`|Uma suspensão do thread foi solicitada.|  
|`USER_BACKGROUND`|O thread está sendo executado em segundo plano.|  
|`USER_UNSTARTED`|O thread não iniciou a execução.|  
|`USER_STOPPED`|O thread foi encerrado.|  
|`USER_WAIT_SLEEP_JOIN`|O thread está aguardando outro thread concluir uma tarefa.|  
|`USER_SUSPENDED`|O thread foi suspenso.|  
|`USER_UNSAFE_POINT`|O thread está em um ponto não seguro. Ou seja, o thread está em um ponto na execução em que ele pode bloquear a coleta de lixo.<br /><br /> Eventos de depuração podem ser expedidos de pontos não seguros, mas suspender um thread em um ponto não seguro provavelmente causará um deadlock até que o thread seja retomado. Os pontos seguros e inseguros são determinados pela implementação JIT (just-in-time) e pela coleta de lixo.|  
|`USER_THREADPOOL`|O thread é do pool de threads.|  
  
## <a name="remarks"></a>Comentários  

 O estado do usuário de um thread é o estado que o thread tem quando o depurador o examina. Um thread pode ter uma combinação de Estados do usuário.  
  
 Use o método [ICorDebugThread:: GetUserState](icordebugthread-getuserstate-method.md) para recuperar o estado do usuário de um thread.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
