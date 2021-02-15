---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: RemotingClientInvocationStarted'
title: Método ICorProfilerCallback::RemotingClientInvocationStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RemotingClientInvocationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RemotingClientInvocationStarted
helpviewer_keywords:
- RemotingClientInvocationStarted method [.NET Framework profiling]
- ICorProfilerCallback::RemotingClientInvocationStarted method [.NET Framework profiling]
ms.assetid: 796b63f3-c809-47f1-89cc-b23ad8eb5e79
topic_type:
- apiref
ms.openlocfilehash: 3727383c3a23fa9e4327970e84c6ebde4ab14db0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99788963"
---
# <a name="icorprofilercallbackremotingclientinvocationstarted-method"></a>Método ICorProfilerCallback::RemotingClientInvocationStarted

Notifica o criador de perfil de que uma chamada de comunicação remota foi iniciada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT RemotingClientInvocationStarted();  
```  
  
## <a name="remarks"></a>Comentários  

 Esse evento é o mesmo para chamadas síncronas e assíncronas.  
  
 Cada um dos seguintes pares de retornos de chamada ocorrerá no mesmo thread:  
  
- `RemotingClientInvocationStarted` e [ICorProfilerCallback:: RemotingClientSendingMessage](icorprofilercallback-remotingclientsendingmessage-method.md)  
  
- [ICorProfilerCallback:: RemotingClientReceivingReply](icorprofilercallback-remotingclientreceivingreply-method.md) e [ICorProfilerCallback:: RemotingClientInvocationFinished](icorprofilercallback-remotingclientinvocationfinished-method.md)  
  
- [ICorProfilerCallback:: RemotingServerInvocationReturned](icorprofilercallback-remotingserverinvocationreturned-method.md) e [ICorProfilerCallback:: RemotingServerSendingReply](icorprofilercallback-remotingserversendingreply-method.md)  
  
 Você deve estar ciente dos seguintes problemas com os retornos de chamada remotos:  
  
- A execução de uma função de comunicação remota não é refletida pela API do criador de perfil, portanto, as notificações para funções que são chamadas do cliente e executadas no servidor não são recebidas corretamente. A invocação real ocorre por meio de um objeto proxy; para o criador de perfil, parece que determinadas funções são compiladas por JIT, mas nunca são usadas.  
  
- O criador de perfil não recebe notificações precisas para eventos de comunicação remota assíncrona.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
