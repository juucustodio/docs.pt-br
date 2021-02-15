---
description: 'Saiba mais sobre: interface ICorDebugVariableSymbol'
title: Interface ICorDebugVariableSymbol
ms.date: 03/30/2017
ms.assetid: 0e58b85e-69bd-41ff-bedb-8cdc8be6a7a2
ms.openlocfilehash: fa3fc1f318627e9175a3066c3bd3eac00929ea60
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790536"
---
# <a name="icordebugvariablesymbol-interface"></a>Interface ICorDebugVariableSymbol

Recupera as informações de símbolo de depuração para uma variável.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetName](icordebugvariablesymbol-getname-method.md)|Obtém o nome de uma variável.|  
|[Método GetSize](icordebugvariablesymbol-getsize-method.md)|Obtém o tamanho de uma variável em bytes.|  
|[Método GetSlotIndex](icordebugvariablesymbol-getslotindex-method.md)|Obtém o índice de slot gerenciado de uma variável local.|  
|[Método GetValue](icordebugvariablesymbol-getvalue-method.md)|Obtém o valor de uma variável como uma matriz de bytes.|  
|[Método SetValue](icordebugvariablesymbol-setvalue-method.md)|Atribui o valor de uma matriz de bytes a uma variável.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Essa interface está disponível somente com .NET Native. Se você implementar essa interface para cenários ICorDebug fora do .NET Native, o Common Language Runtime ignorará essa interface.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
