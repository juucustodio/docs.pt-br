---
description: 'Saiba mais sobre: interface ICorDebugHeapValue3'
title: Interface ICorDebugHeapValue3
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue3
helpviewer_keywords:
- ICorDebugHeapValue3 interface [.NET Framework debugging]
ms.assetid: 9c421bb0-e647-4b2d-a986-f3d578cc7f20
topic_type:
- apiref
ms.openlocfilehash: 2483f74e2cfc105fd23c37af6ada467f17b9556b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791459"
---
# <a name="icordebugheapvalue3-interface"></a>Interface ICorDebugHeapValue3

Expõe as propriedades de bloqueio de monitoramento de objetos. Essa interface estende as interfaces ICorDebugHeapValue e ICorDebugHeapValue2.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetThreadOwningMonitorLock](icordebugheapvalue3-getthreadowningmonitorlock-method.md)|Retorna o thread gerenciado que possui o bloqueio de monitor neste objeto.|  
|[Método GetMonitorEventWaitList](icordebugheapvalue3-getmonitoreventwaitlist-method.md)|Fornece uma lista ordenada de threads que são enfileirados no evento que está associado a um bloqueio de monitor.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
