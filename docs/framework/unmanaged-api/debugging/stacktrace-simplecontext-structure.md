---
description: 'Saiba mais sobre: estrutura de StackTrace_SimpleContext'
title: Estrutura StackTrace_SimpleContext
ms.date: 03/30/2017
api_name:
- StackTrace_SimpleContext
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- SimpleContext
helpviewer_keywords:
- SimpleContext structure [.NET Framework debugging]
- StackTrace_SimpleContext structure [.NET Framework debugging]
ms.assetid: d4cef11f-a8ca-49bc-a1b8-6631f9e28f3e
topic_type:
- apiref
ms.openlocfilehash: 22a0acada5ef2d392dfdef5326953be137280d7f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800546"
---
# <a name="stacktrace_simplecontext-structure"></a>Estrutura StackTrace_SimpleContext

Fornece um contexto simples que pode ser usado em lugar de uma estrutura `CONTEXT` completa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
struct StackTrace_SimpleContext  
{  
    ULONG64 StackOffset;       // ESP on x86  
    ULONG64 FrameOffset;       // EBP on x86  
    ULONG64 InstructionOffset; // EIP on x86  
};  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`StackOffset`|O ponteiro de pilha ou o ponteiro de pilha Enter (ESP) em plataformas x86.|  
|`FrameOffset`|O deslocamento do quadro ou o EBP se registra em plataformas x86.|  
|`InstructionOffset`|O ponteiro de instrução ou o EIP (ponteiro de instrução Enter) em plataformas x86.|  
  
## <a name="remarks"></a>Comentários  

 Como as funções de rastreamento de pilha normalmente precisam retornar apenas o endereço, o deslocamento do quadro e o endereço da pilha, você pode, opcionalmente, usar a `SimpleContext` estrutura em vez de uma `CONTEXT` estrutura grande.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** SOS_Stacktrace. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
