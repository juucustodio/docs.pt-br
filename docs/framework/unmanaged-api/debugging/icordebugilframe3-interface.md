---
description: 'Saiba mais sobre: interface ICorDebugILFrame3'
title: Interface ICorDebugILFrame3
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame3
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 15212cb5-93d4-4025-bec9-d4b9919eb1fe
topic_type:
- apiref
ms.openlocfilehash: a34a3f0941871a2d0a63fb2d9f78ccb7ff455866
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791251"
---
# <a name="icordebugilframe3-interface"></a>Interface ICorDebugILFrame3

Fornece um método que encapsula o valor de retorno de uma função. `ICorDebugILFrame3` é uma extensão lógica das interfaces ICorDebugILFrame e ICorDebugILFrame2.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetReturnValueForILOffset](icordebugilframe3-getreturnvalueforiloffset-method.md)|Obtém um objeto ICorDebugValue que encapsula o valor de retorno de uma função.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugCode3](icordebugcode3-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
