---
description: 'Saiba mais sobre: interface ICorDebugController'
title: Interface ICorDebugController
ms.date: 03/30/2017
api_name:
- ICorDebugController
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController
helpviewer_keywords:
- ICorDebugController interface [.NET Framework debugging]
ms.assetid: dbb1c4dc-269a-459b-ab1d-6c70788782ce
topic_type:
- apiref
ms.openlocfilehash: 588c41b5b8d87589facd6085655ed0ad415ec3aa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710745"
---
# <a name="icordebugcontroller-interface"></a>Interface ICorDebugController

Representa um escopo, um <xref:System.Diagnostics.Process> ou um <xref:System.AppDomain>, em que o contexto de execução de código pode ser controlado.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|`ICorDebugController::CanCommitChanges`|Esse método é obsoleto.|  
|`ICorDebugController::CommitChanges`|Esse método é obsoleto.|  
|[Método Continue](icordebugcontroller-continue-method.md)|Retoma a execução de threads gerenciados após uma chamada para [ICorDebugController:: Stop](icordebugcontroller-stop-method.md).|  
|[Método Detach](icordebugcontroller-detach-method.md)|Desanexa o depurador do domínio do processo ou do aplicativo.|  
|[Método EnumerateThreads](icordebugcontroller-enumeratethreads-method.md)|Obtém um enumerador para os threads gerenciados ativos no processo.|  
|[Método HasQueuedCallbacks](icordebugcontroller-hasqueuedcallbacks-method.md)|Obtém um valor que indica se qualquer retorno de chamada gerenciado está na fila no momento para o thread especificado.|  
|[Método IsRunning](icordebugcontroller-isrunning-method.md)|Obtém um valor que indica se os threads no processo estão em execução livremente no momento.|  
|[Método SetAllThreadsDebugState](icordebugcontroller-setallthreadsdebugstate-method.md)|Define o estado de depuração de todos os threads gerenciados no processo.|  
|[Método Stop](icordebugcontroller-stop-method.md)|Executa uma parada cooperativa em todos os threads que estão executando código gerenciado no processo.|  
|[Método Terminate](icordebugcontroller-terminate-method.md)|Encerra o processo com o código de saída especificado.|  
  
## <a name="remarks"></a>Comentários  

 Se `ICorDebugController` o estiver controlando um processo, o escopo incluirá todos os threads do processo. Se `ICorDebugController` o estiver controlando um domínio de aplicativo, o escopo incluirá somente os threads desse domínio de aplicativo específico.  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
