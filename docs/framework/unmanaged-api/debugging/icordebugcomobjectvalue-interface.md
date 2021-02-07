---
description: 'Saiba mais sobre: interface ICorDebugComObjectValue'
title: Interface ICorDebugComObjectValue
ms.date: 03/30/2017
api_name:
- ICorDebugComObjectValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugComObjectValue
helpviewer_keywords:
- ICorDebugComObjectValue interface [.NET Framework debugging]
ms.assetid: 505a7f6c-d92b-42b4-b539-433f5102ea9b
topic_type:
- apiref
ms.openlocfilehash: 3c071c371ae6e330431630cfb1934b538d62efe6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710810"
---
# <a name="icordebugcomobjectvalue-interface"></a>Interface ICorDebugComObjectValue

Fornece métodos para recuperar informações associadas a um RCW (Runtime Callable Wrapper).  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetCachedInterfacePointers](icordebugcomobjectvalue-getcachedinterfacepointers-method.md)|Obtém os ponteiros de interface bruto armazenados em cache no RCW atual.|  
|[Método GetCachedInterfaceTypes](icordebugcomobjectvalue-getcachedinterfacetypes-method.md)|Fornece um enumerador para os tipos de interface para os quais o objeto atual foi usado em maiúsculas ou usados.|  
  
## <a name="remarks"></a>Comentários  

 Para verificar se uma instância de uma interface "ICorDebugValue" representa um RCW, um depurador chama `QueryInterface` "ICorDebugValue" com `IID_ICorDebugComObjectValue` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
