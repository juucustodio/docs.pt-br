---
description: 'Saiba mais sobre: interface ICLRSyncManager'
title: Interface ICLRSyncManager
ms.date: 03/30/2017
api_name:
- ICLRSyncManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRSyncManager
helpviewer_keywords:
- ICLRSyncManager interface [.NET Framework hosting]
ms.assetid: a49f9d80-1c76-4ddd-8c49-34f913a5c596
topic_type:
- apiref
ms.openlocfilehash: 188d1c913d75666aea09b17244012401d377fa10
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784994"
---
# <a name="iclrsyncmanager-interface"></a>Interface ICLRSyncManager

Define métodos que permitem ao host obter informações sobre as tarefas solicitadas e para detectar deadlocks em sua implementação de sincronização.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CreateRWLockOwnerIterator](iclrsyncmanager-createrwlockowneriterator-method.md)|Solicita que o Common Language Runtime (CLR) crie um iterador para o host usar para determinar o conjunto de tarefas que estão aguardando um bloqueio do gravador de leitor.|  
|[Método DeleteRWLockOwnerIterator](iclrsyncmanager-deleterwlockowneriterator-method.md)|Solicita que o CLR destrua um iterador criado por uma chamada para `CreateRWLockOwnerIterator` .|  
|[Método GetMonitorOwner](iclrsyncmanager-getmonitorowner-method.md)|Obtém a tarefa que possui o monitor especificado.|  
|[Método GetRWLockOwnerNext](iclrsyncmanager-getrwlockownernext-method.md)|Obtém a próxima tarefa que está aguardando o bloqueio do gravador de leitor atual.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Threading.Thread>
- [Interface IHostSyncManager](ihostsyncmanager-interface.md)
- [Threading gerenciado e não gerenciado](/previous-versions/dotnet/netframework-4.0/5s8ee185(v=vs.100))
- [Interfaces de hospedagem](hosting-interfaces.md)
