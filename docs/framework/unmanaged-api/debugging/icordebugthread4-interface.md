---
description: 'Saiba mais sobre: interface ICorDebugThread4'
title: Interface ICorDebugThread4
ms.date: 03/30/2017
api_name:
- ICorDebugThread4
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread4
helpviewer_keywords:
- ICorDebugThread4 interface [.NET Framework debugging]
ms.assetid: a8c7719a-322b-4133-8566-4c27218dc104
topic_type:
- apiref
ms.openlocfilehash: 4ad587cee81ce635df0a8917b7a6d68e60aaf0b3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800910"
---
# <a name="icordebugthread4-interface"></a>Interface ICorDebugThread4

Fornece informações de bloqueio de thread.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetBlockingObjects](icordebugthread4-getblockingobjects-method.md)|Fornece uma enumeração ordenada de estruturas [CorDebugBlockingObject](cordebugblockingobject-structure.md) que fornecem informações de bloqueio de thread.|  
|[Método HadUnhandledException](icordebugthread4-hadunhandledexception-method.md)|Indica se o thread já teve uma exceção sem tratamento.|  
|[Método GetCurrentCustomDebuggerNotification](icordebugthread4-getcurrentcustomdebuggernotification-method.md)|Obtém o objeto [ICorDebugManagedCallback3:: CustomNotification](icordebugmanagedcallback3-customnotification-method.md) atual no thread atual.|  
  
## <a name="remarks"></a>Comentários  

 Essa interface é uma extensão lógica das interfaces ICorDebugThread, ICorDebugThread2 e [ICorDebugThread3](icordebugthread3-interface.md) .  
  
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
