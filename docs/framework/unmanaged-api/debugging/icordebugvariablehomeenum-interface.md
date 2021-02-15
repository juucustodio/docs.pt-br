---
description: 'Saiba mais sobre: interface ICorDebugVariableHomeEnum'
title: Interface ICorDebugVariableHomeEnum
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHomeEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHomeEnum
helpviewer_keywords:
- ICorDebugVariableHomeEnum interface [.NET Framework debugging]
ms.assetid: c312ae6d-c8dc-48d6-9f1e-ead515c88fdf
topic_type:
- apiref
ms.openlocfilehash: c56c68a6b5f9d329fe8af23f47b40fa629bfe3ba
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790614"
---
# <a name="icordebugvariablehomeenum-interface"></a>Interface ICorDebugVariableHomeEnum

Fornece um enumerador para as variáveis locais e argumentos em uma função.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Next](icordebugvariablehomeenum-next-method.md)|Obtém o número especificado de instâncias [ICorDebugVariableHome](icordebugvariablehome-interface.md) que contêm informações sobre as variáveis e os argumentos locais em uma função.|  
  
## <a name="remarks"></a>Comentários  

 A `ICorDebugVariableHomeEnum` interface implementa a interface ICorDebugEnum.  
  
 Uma `ICorDebugVariableHomeEnum` instância é populada com instâncias [ICorDebugVariableHome](icordebugvariablehome-interface.md) chamando o método [ICorDebugCode4:: EnumerateVariableHomes](icordebugcode4-enumeratevariablehomes-method.md) . Cada instância de [ICorDebugVariableHome](icordebugvariablehome-interface.md) na coleção representa uma variável local ou um argumento em uma função. Os objetos  [ICorDebugVariableHome](icordebugvariablehome-interface.md) na coleção podem ser enumerados chamando o método [ICorDebugVariableHomeEnum:: Next](icordebugvariablehomeenum-next-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugVariableHome](icordebugvariablehome-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
