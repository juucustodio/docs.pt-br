---
description: 'Saiba mais sobre: interface ICorDebugThread2'
title: Interface ICorDebugThread2
ms.date: 03/30/2017
api_name:
- ICorDebugThread2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2
helpviewer_keywords:
- ICorDebugThread2 interface [.NET Framework debugging]
ms.assetid: 678f89f9-cce7-46d1-af87-5e989abaa93c
topic_type:
- apiref
ms.openlocfilehash: 81f687f6daff9ffa7298ec6d818a214b8934bcc3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658481"
---
# <a name="icordebugthread2-interface"></a>Interface ICorDebugThread2

Serve como uma extensão lógica para a interface ICorDebugThread.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetActiveFunctions](icordebugthread2-getactivefunctions-method.md)|Obtém uma matriz de instâncias de COR_ACTIVE_FUNCTION que contêm dados sobre as funções ativas nos quadros de um thread.|  
|[Método GetConnectionID](icordebugthread2-getconnectionid-method.md)|Obtém um identificador de conexão para isso `ICorDebugThread2` .|  
|[Método GetTaskID](icordebugthread2-gettaskid-method.md)|Obtém um identificador de tarefa para isso `ICorDebugThread2` .|  
|[Método GetVolatileOSThreadID](icordebugthread2-getvolatileosthreadid-method.md)|Obtém o identificador de thread do sistema operacional para isso `ICorDebugThread2` .|  
|[Método InterceptCurrentException](icordebugthread2-interceptcurrentexception-method.md)|Permite que um depurador intercepte a exceção atual em um thread.|  
  
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
