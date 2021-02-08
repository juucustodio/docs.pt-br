---
description: 'Saiba mais sobre: interface ICorDebugILFrame'
title: Interface ICorDebugILFrame
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame
helpviewer_keywords:
- ICorDebugILFrame interface [.NET Framework debugging]
ms.assetid: d5cf5056-da4d-4629-914d-afe42a5393df
topic_type:
- apiref
ms.openlocfilehash: 251fa18151ff286bee3e1bcf7707bf5f7145b4f1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791342"
---
# <a name="icordebugilframe-interface"></a>Interface ICorDebugILFrame

Representa um quadro de pilha do código MSIL (Microsoft Intermediate Language). Essa interface é uma subclasse da interface ICorDebugFrame.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CanSetIP](icordebugilframe-cansetip-method.md)|Obtém um valor que indica se é seguro definir o ponteiro de instrução para o local de deslocamento especificado.|  
|[Método EnumerateArguments](icordebugilframe-enumeratearguments-method.md)|Obtém um enumerador para os argumentos neste quadro.|  
|[Método EnumerateLocalVariables](icordebugilframe-enumeratelocalvariables-method.md)|Obtém um enumerador para as variáveis locais neste quadro.|  
|[Método GetArgument](icordebugilframe-getargument-method.md)|Obtém o valor do argumento especificado neste quadro de pilha MSIL.|  
|[Método GetIP](icordebugilframe-getip-method.md)|Obtém o valor do ponteiro de instrução e um valor de combinação de bits que descreve como o valor do ponteiro de instrução foi obtido.|  
|[Método GetLocalVariable](icordebugilframe-getlocalvariable-method.md)|Obtém o valor da variável local especificada neste quadro da pilha MSIL.|  
|[Método GetStackDepth](icordebugilframe-getstackdepth-method.md)|Não implementado.|  
|[Método GetStackValue](icordebugilframe-getstackvalue-method.md)|Não implementado.|  
|[Método SetIP](icordebugilframe-setip-method.md)|Define o ponteiro de instrução para o local de deslocamento especificado no código MSIL.|  
  
## <a name="remarks"></a>Comentários  

 A `ICorDebugILFrame` interface é uma interface ICorDebugFrame especializada. Ele é usado para quadros de código MSIL ou para quadros compilados just-in-time (JIT). Os quadros compilados em JIT implementam a interface `ICorDebugILFrame` e a interface ICorDebugNativeFrame.  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
