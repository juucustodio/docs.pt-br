---
description: 'Saiba mais sobre: interface IHostTask'
title: Interface IHostTask
ms.date: 03/30/2017
api_name:
- IHostTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask
helpviewer_keywords:
- IHostTask interface [.NET Framework hosting]
ms.assetid: a71dbbd5-64b8-47eb-9f03-8e8c85fbe2bc
topic_type:
- apiref
ms.openlocfilehash: c46bbdd2e881c20d1ffd634bec8ddfa3b70b0f82
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784659"
---
# <a name="ihosttask-interface"></a>Interface IHostTask

Fornece métodos que permitem que o Common Language Runtime (CLR) se comunique com o host para gerenciar tarefas.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Alert](ihosttask-alert-method.md)|Solicita que o host ative a tarefa representada pela instância atual `IHostTask` , para que a tarefa possa ser anulada.|  
|[Método GetPriority](ihosttask-getpriority-method.md)|Obtém o nível de prioridade do thread da tarefa representada pela `IHostTask` instância atual.|  
|[Método Join](ihosttask-join-method.md)|Bloqueia a tarefa de chamada até que a tarefa representada pela `IHostTask` instância atual seja concluída, o intervalo de tempo especificado decorre ou [IHostTask:: Alert](ihosttask-alert-method.md) seja chamado.|  
|[Método SetCLRTask](ihosttask-setclrtask-method.md)|Associa uma instância de [interface ICLRTask](iclrtask-interface.md) à `IHostTask` instância atual.|  
|[Método SetPriority](ihosttask-setpriority-method.md)|Solicita que o host ajuste o nível de prioridade de thread para a tarefa representada pela `IHostTask` instância atual.|  
|[Método Start](ihosttask-start-method.md)|Solicita que o host mova a tarefa representada pela instância atual `IHostTask` de um estado suspenso para um estado ativo, no qual o código pode ser executado.|  
  
## <a name="remarks"></a>Comentários  

 O CLR chama os métodos definidos pelo `IHostTask` para iniciar uma tarefa, definir seu nível de prioridade de thread e assim por diante.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRTask](iclrtask-interface.md)
- [Interface ICLRTaskManager](iclrtaskmanager-interface.md)
- [Interface IHostTaskManager](ihosttaskmanager-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
