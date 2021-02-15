---
description: 'Saiba mais sobre: interface ICorDebugILFrame4'
title: Interface ICorDebugILFrame4
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame4
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 1e739183-3e05-49e5-846f-4075256e41de
topic_type:
- apiref
ms.openlocfilehash: f2d29229f039509ed7799399f0d4d701e8cafba7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791199"
---
# <a name="icordebugilframe4-interface"></a>Interface ICorDebugILFrame4

[Com suporte no .NET Framework 4.5.2 e versões posteriores]  
  
 Fornece métodos que permitem acessar as variáveis locais e inserir o código em um registro de ativação de código IL. Um parâmetro especifica se o depurador possui acesso às variáveis e ao código adicionados na instrumentação do criador de perfil ReJIT.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método EnumerateLocalVariablesEx](icordebugilframe4-enumeratelocalvariablesex-method.md)|Retorna uma lista das variáveis locais disponíveis em um quadro atual.|  
|[Método GetCodeEx](icordebugilframe4-getcodeex-method.md)|Retorna o código que esse quadro de pilha está executando.|  
|[Método GetLocalVariableEx](icordebugilframe4-getlocalvariableex-method.md)|Retorna o valor de uma variável local no quadro IL.|  
  
## <a name="remarks"></a>Comentários  

 Esses métodos oferecem funcionalidade além da fornecida pelos métodos [EnumerateLocalVariables](icordebugilframe-enumeratelocalvariables-method.md), [GetCode](icordebugframe-getcode-method.md)e [GetLocalVariable](icordebugilframe-getlocalvariable-method.md) . Cada método inclui um parâmetro `flags` que especifica se as variáveis locais adicionais ou o código definido por uma solicitação do ReJIT do criador de perfil estão visíveis.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
