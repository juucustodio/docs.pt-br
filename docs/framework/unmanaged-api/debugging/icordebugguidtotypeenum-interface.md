---
description: 'Saiba mais sobre: interface ICorDebugGuidToTypeEnum'
title: Interface ICorDebugGuidToTypeEnum
ms.date: 03/30/2017
api_name:
- ICorDebugGuidToTypeEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGuidToTypeEnum
helpviewer_keywords:
- ICorDebugGuidToTypeEnum interface [.NET Framework debugging]
ms.assetid: aa32b12b-05fc-4ea8-a904-adae25034269
topic_type:
- apiref
ms.openlocfilehash: abcdc9537f6f6ff2e0ac9b2be86734efbf303493
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99660980"
---
# <a name="icordebugguidtotypeenum-interface"></a>Interface ICorDebugGuidToTypeEnum

Fornece um enumerador que define o mapeamento entre um conjunto de GUIDs e seus tipos correspondentes, que são representados por instâncias de ICorDebugType. Essa interface herda os métodos da interface ICorDebugEnum.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[ICorDebugGuidToTypeEnum:: Next](icordebugguidtotypeenum-next-method.md)|Obtém o número especificado de instâncias de [CorDebugGuidToTypeMapping](cordebugguidtotypemapping-structure.md) que MAPEIAm GUIDs para informações de tipo.|  
  
## <a name="remarks"></a>Comentários  

 Um `ICorDebugGuidToTypeEnum` objeto de interface pode ser recuperado chamando o método [ICorDebugAppDomain3:: GetCachedWinRTTypes](icordebugappdomain3-getcachedwinrttypes-method.md) . Um depurador pode chamar o [próximo](icordebugguidtotypeenum-next-method.md) método da interface para recuperar objetos [CorDebugGuidToTypeMapping](cordebugguidtotypemapping-structure.md) que representam mapeamentos de representações gerenciadas de tipos de Windows Runtime carregados no domínio de aplicativo usado para a chamada para o método [ICorDebugAppDomain3:: GetCachedWinRTTypes](icordebugappdomain3-getcachedwinrttypes-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** Windows Runtime  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
