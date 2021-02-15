---
description: 'Saiba mais sobre: interface ICorDebugValue3'
title: Interface ICorDebugValue3
ms.date: 03/30/2017
api_name:
- ICorDebugValue3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue3
helpviewer_keywords:
- ICorDebugValue3 interface [.NET Framework debugging]
ms.assetid: 7d5385d3-f4a5-47c4-8478-a3513b5e9406
topic_type:
- apiref
ms.openlocfilehash: e5868b91d23426a2d8dd8fed87b13ec61fef95ef
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794644"
---
# <a name="icordebugvalue3-interface"></a>Interface ICorDebugValue3

Estende as interfaces "ICorDebugValue" e "ICorDebugValue2" para fornecer suporte a matrizes com mais de 2 GB.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetSize64](icordebugvalue3-getsize64-method.md)|Obtém o tamanho, em bytes, deste `ICorDebugValue3` objeto.|  
  
## <a name="remarks"></a>Comentários  

 O método [ICorDebugValue:: GetSize](icordebugvalue3-getsize64-method.md) retorna um tamanho de objeto que varia de 0 a 2.147.483.647 bytes. No .NET Framework 4,5, o tamanho das matrizes pode exceder 2 GB. A `ICorDebugValue3` interface permite que você determine o tamanho dessas matrizes.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
