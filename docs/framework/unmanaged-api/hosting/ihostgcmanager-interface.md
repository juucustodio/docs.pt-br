---
description: 'Saiba mais sobre: interface IHostGCManager'
title: Interface IHostGCManager
ms.date: 03/30/2017
api_name:
- IHostGCManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostGCManager
helpviewer_keywords:
- IHostGCManager interface [.NET Framework hosting]
ms.assetid: 820330a4-244c-4f67-ab5e-f24b0b3c2080
topic_type:
- apiref
ms.openlocfilehash: da229c04eb5f5a27c34c133b5c88183d00f47c40
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99708652"
---
# <a name="ihostgcmanager-interface"></a>Interface IHostGCManager

Fornece métodos que notificam o host de eventos no mecanismo de coleta de lixo implementado pelo Common Language Runtime (CLR).  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|[Método SuspensionEnding](ihostgcmanager-suspensionending-method.md)|Notifica o host de que o CLR está retomando a execução de tarefas em threads que foram suspensos para uma coleta de lixo.|  
|[Método SuspensionStarting](ihostgcmanager-suspensionstarting-method.md)|Notifica o host de que o CLR está suspendendo a execução de tarefas, para executar uma coleta de lixo.|  
|[Método ThreadIsBlockingForSuspension](ihostgcmanager-threadisblockingforsuspension-method.md)|Notifica o host de que o thread do qual a chamada de método foi feita está prestes a ser bloqueado para uma coleta de lixo.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRTask](iclrtask-interface.md)
- [Interface ICLRTaskManager](iclrtaskmanager-interface.md)
- [Interface IHostTask](ihosttask-interface.md)
- [Interface IHostTaskManager](ihosttaskmanager-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
