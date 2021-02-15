---
description: 'Saiba mais sobre: interface ICorDebugValue2'
title: Interface ICorDebugValue2
ms.date: 03/30/2017
api_name:
- ICorDebugValue2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue2
helpviewer_keywords:
- ICorDebugValue2 interface [.NET Framework debugging]
ms.assetid: 3ff2ad2a-da5a-461b-8627-1a8eba49df9c
topic_type:
- apiref
ms.openlocfilehash: b408bb5d1732a60fc9aa8ffb93321d3542f2cab7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690256"
---
# <a name="icordebugvalue2-interface"></a>Interface ICorDebugValue2

Estende a interface "ICorDebugValue" para fornecer suporte para objetos "ICorDebugType".  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetExactType](icordebugvalue2-getexacttype-method.md)|Obtém um ponteiro de interface para um `ICorDebugType` objeto que representa o <xref:System.Type> desse valor.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)

- [Interface ICorDebugValue3](icordebugvalue3-interface.md)
