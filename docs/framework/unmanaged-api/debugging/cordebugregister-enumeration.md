---
description: 'Saiba mais sobre: Enumeração CorDebugRegister'
title: Enumeração CorDebugRegister
ms.date: 03/30/2017
api_name:
- CorDebugRegister
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugRegister
helpviewer_keywords:
- CorDebugRegister enumeration [.NET Framework debugging]
ms.assetid: 003bb138-7960-4291-ac88-0d87e470ff70
topic_type:
- apiref
ms.openlocfilehash: 7a5dc771a239a82448f898e2f518e920993ec35a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661864"
---
# <a name="cordebugregister-enumeration"></a>Enumeração CorDebugRegister

Especifica os registros associados a uma determinada arquitetura de processador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugRegister {  
  
    REGISTER_INSTRUCTION_POINTER = 0,  
    REGISTER_STACK_POINTER,  
    REGISTER_FRAME_POINTER,  
  
    REGISTER_X86_EIP = 0,  
    REGISTER_X86_ESP,  
    REGISTER_X86_EBP,  
  
    REGISTER_X86_EAX,  
    REGISTER_X86_ECX,  
    REGISTER_X86_EDX,  
    REGISTER_X86_EBX,  
  
    REGISTER_X86_ESI,  
    REGISTER_X86_EDI,  
  
    REGISTER_X86_FPSTACK_0,  
    REGISTER_X86_FPSTACK_1,  
    REGISTER_X86_FPSTACK_2,  
    REGISTER_X86_FPSTACK_3,  
    REGISTER_X86_FPSTACK_4,  
    REGISTER_X86_FPSTACK_5,  
    REGISTER_X86_FPSTACK_6,  
    REGISTER_X86_FPSTACK_7,  
  
    REGISTER_AMD64_RIP = 0,  
    REGISTER_AMD64_RSP,  
    REGISTER_AMD64_RBP,  
    REGISTER_AMD64_RAX,  
    REGISTER_AMD64_RCX,  
    REGISTER_AMD64_RDX,  
    REGISTER_AMD64_RBX,  
    REGISTER_AMD64_RSI,  
    REGISTER_AMD64_RDI,  
    REGISTER_AMD64_R8,  
    REGISTER_AMD64_R9,  
    REGISTER_AMD64_R10,  
    REGISTER_AMD64_R11,  
    REGISTER_AMD64_R12,  
    REGISTER_AMD64_R13,  
    REGISTER_AMD64_R14,  
    REGISTER_AMD64_R15,  
  
    REGISTER_AMD64_XMM0,  
    REGISTER_AMD64_XMM1,  
    REGISTER_AMD64_XMM2,  
    REGISTER_AMD64_XMM3,  
    REGISTER_AMD64_XMM4,  
    REGISTER_AMD64_XMM5,  
    REGISTER_AMD64_XMM6,  
    REGISTER_AMD64_XMM7,  
    REGISTER_AMD64_XMM8,  
    REGISTER_AMD64_XMM9,  
    REGISTER_AMD64_XMM10,  
    REGISTER_AMD64_XMM11,  
    REGISTER_AMD64_XMM12,  
    REGISTER_AMD64_XMM13,  
    REGISTER_AMD64_XMM14,  
    REGISTER_AMD64_XMM15,  
  
    REGISTER_IA64_BSP = REGISTER_FRAME_POINTER,  
    REGISTER_IA64_R0  = REGISTER_IA64_BSP + 1,  
    REGISTER_IA64_F0  = REGISTER_IA64_R0  + 128,  
    REGISTER_ARM_PC = 0,  
    REGISTER_ARM_SP,  
    REGISTER_ARM_R0,  
    REGISTER_ARM_R1,  
    REGISTER_ARM_R2,  
    REGISTER_ARM_R3,  
    REGISTER_ARM_R4,  
    REGISTER_ARM_R5,  
    REGISTER_ARM_R6,  
    REGISTER_ARM_R7,  
    REGISTER_ARM_R8,  
    REGISTER_ARM_R9,  
    REGISTER_ARM_R10,  
    REGISTER_ARM_R11,  
    REGISTER_ARM_R12,  
    REGISTER_ARM_LR,  
  
} CorDebugRegister;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`REGISTER_INSTRUCTION_POINTER`|Um registro de ponteiro de instrução em qualquer processador.|  
|`REGISTER_STACK_POINTER`|Um registro de ponteiro de pilha em qualquer processador.|  
|`REGISTER_FRAME_POINTER`|Um registro de ponteiro de quadro em qualquer processador.|  
|`REGISTER_X86_EIP`|O registro de ponteiro de instrução no processador x86.|  
|`REGISTER_X86_ESP`|O registro de ponteiro de pilha no processador x86.|  
|`REGISTER_X86_EBP`|O registro de ponteiro de base no processador x86.|  
|`REGISTER_X86_EAX`|O registro de dados A no processador x86.|  
|`REGISTER_X86_ECX`|O registro de dados C no processador x86.|  
|`REGISTER_X86_EDX`|O registro de dados D no processador x86.|  
|`REGISTER_X86_EBX`|O registro de dados B no processador x86.|  
|`REGISTER_X86_ESI`|O registro de índice de origem no processador x86.|  
|`REGISTER_X86_EDI`|O registro de índice de destino no processador x86.|  
|`REGISTER_X86_FPSTACK_0`|O registro de pilha 0 no processador x86 de ponto flutuante (FP).|  
|`REGISTER_X86_FPSTACK_1`|O registro de pilha #1 no processador x86 de FP.|  
|`REGISTER_X86_FPSTACK_2`|O registro de pilha #2 no processador x86 de FP.|  
|`REGISTER_X86_FPSTACK_3`|O registro de pilha #3 no processador x86 de FP.|  
|`REGISTER_X86_FPSTACK_4`|O registro de pilha #4 no processador x86 de FP.|  
|`REGISTER_X86_FPSTACK_5`|O registro de pilha #5 no processador x86 de FP.|  
|`REGISTER_X86_FPSTACK_6`|O registro de pilha #6 no processador x86 de FP.|  
|`REGISTER_X86_FPSTACK_7`|O registro de pilha #7 no processador x86 de FP.|  
|`REGISTER_AMD64_RIP`|O registro de ponteiro de instrução no processador AMD64.|  
|`REGISTER_AMD64_RSP`|O registro de ponteiro de pilha no processador AMD64.|  
|`REGISTER_AMD64_RBP`|O registro de ponteiro de base no processador AMD64.|  
|`REGISTER_AMD64_RAX`|O registro de dados A no processador AMD64.|  
|`REGISTER_AMD64_RCX`|O registro de dados C no processador AMD64.|  
|`REGISTER_AMD64_RDX`|O registro de dados D no processador AMD64.|  
|`REGISTER_AMD64_RBX`|O registro de dados B no processador AMD64.|  
|`REGISTER_AMD64_RSI`|O registro de índice de origem no processador AMD64.|  
|`REGISTER_AMD64_RDI`|O registro de índice de destino no processador AMD64.|  
|`REGISTER_AMD64_R8`|O registro de dados #8 no processador AMD64.|  
|`REGISTER_AMD64_R9`|O registro de dados #9 no processador AMD64.|  
|`REGISTER_AMD64_R10`|O registro de dados #10 no processador AMD64.|  
|`REGISTER_AMD64_R11`|O registro de dados #11 no processador AMD64.|  
|`REGISTER_AMD64_R12`|O registro de dados #12 no processador AMD64.|  
|`REGISTER_AMD64_R13`|O registro de dados #13 no processador AMD64.|  
|`REGISTER_AMD64_R14`|O registro de dados #14 no processador AMD64.|  
|`REGISTER_AMD64_R15`|O registro de dados #15 no processador AMD64.|  
|`REGISTER_AMD64_XMM0`|O registro de multimídia #0 no processador AMD64.|  
|`REGISTER_AMD64_XMM1`|O registro de multimídia #1 no processador AMD64.|  
|`REGISTER_AMD64_XMM2`|O registro de multimídia #2 no processador AMD64.|  
|`REGISTER_AMD64_XMM3`|O registro de multimídia #3 no processador AMD64.|  
|`REGISTER_AMD64_XMM4`|O registro de multimídia #4 no processador AMD64.|  
|`REGISTER_AMD64_XMM5`|O registro de multimídia #5 no processador AMD64.|  
|`REGISTER_AMD64_XMM6`|O registro de multimídia #6 no processador AMD64.|  
|`REGISTER_AMD64_XMM7`|O registro de multimídia #7 no processador AMD64.|  
|`REGISTER_AMD64_XMM8`|O registro de multimídia #8 no processador AMD64.|  
|`REGISTER_AMD64_XMM9`|O registro de multimídia #9 no processador AMD64.|  
|`REGISTER_AMD64_XMM10`|O registro de multimídia #10 no processador AMD64.|  
|`REGISTER_AMD64_XMM11`|O registro de multimídia #11 no processador AMD64.|  
|`REGISTER_AMD64_XMM12`|O registro de multimídia #12 no processador AMD64.|  
|`REGISTER_AMD64_XMM13`|O registro de multimídia #13 no processador AMD64.|  
|`REGISTER_AMD64_XMM14`|O registro de multimídia #14 no processador AMD64.|  
|`REGISTER_AMD64_XMM15`|O registro de multimídia #15 no processador AMD64.|  
|`REGISTER_IA64_BSP`|O registro de ponteiro de pilha no processador IA-64.|  
|`REGISTER_IA64_R0`|O registro de dados #0 no processador IA-64.|  
|`REGISTER_IA64_F0`|O registro de dados de FP #0 no processador IA-64.|  
|`REGISTER_ARM_PC`|O registro do contador de programa (R15) no processador ARM.|  
|`REGISTER_ARM_SP`|O registro do ponteiro de pilha (R13) no processador ARM.|  
|`REGISTER_ARM_R0`|Registro de dados R0 no processador ARM.|  
|`REGISTER_ARM_R1`|Registro de dados R1 no processador ARM.|  
|`REGISTER_ARM_R2`|Registro de dados R2 no processador ARM.|  
|`REGISTER_ARM_R3`|Registro de dados R3 no processador ARM.|  
|`REGISTER_ARM_R4`|Registro R4 no processador ARM.|  
|`REGISTER_ARM_R5`|Registro R5 no processador ARM.|  
|`REGISTER_ARM_R6`|Registro R6 no processador ARM.|  
|`REGISTER_ARM_R7`|O registro R7 (o ponteiro de quadro THuMB) no processador ARM.|  
|`REGISTER_ARM_R8`|Registro R8 no processador ARM.|  
|`REGISTER_ARM_R9`|Registro R9 no processador ARM.|  
|`REGISTER_ARM_R10`|Registro R10 no processador ARM.|  
|`REGISTER_ARM_R11`|O ponteiro de quadro no processador ARM.|  
|`REGISTER_ARM_R12`|Registro R12 no processador ARM.|  
|`REGISTER_ARM_LR`|O registro de vínculo (R14) no processador ARM.|  
  
## <a name="remarks"></a>Comentários  

 Existem 128 registros de dados de uso geral e 128 registros de dados de ponto flutuante no processador IA-64, porém, apenas os valores `REGISTER_IA64_R0` e `REGISTER_IA64_F0` são fornecidos. Os outros valores podem ser determinados da seguinte maneira:  
  
- Some o número do registro ao `REGISTER_IA64_R0` para os valores `REGISTER_IA64_R1` até `REGISTER_IA64_R127`, que correspondem ao registro de dados #1 até o registro de dados #127 no processador IA-64.  
  
- Some o número do registro ao `REGISTER_IA64_F0` para os valores `REGISTER_IA64_F1` até `REGISTER_IA64_F127`, que correspondem ao registro de dados de FP #1 até o registro de dados de FP #127 no processador IA-64.  
  
 Por exemplo, se for necessário especificar o registro de dados #83 no processador IA-64, use `REGISTER_IA64_R0` + 83.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
