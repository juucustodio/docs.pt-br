---
description: 'Saiba mais sobre: interface ICLRTask2'
title: Interface ICLRTask2
ms.date: 03/30/2017
api_name:
- ICLRTask2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2
helpviewer_keywords:
- ICLRTask2 interface [.NET Framework hosting]
ms.assetid: b5a22ebc-0582-49de-91f9-97a3d9789290
topic_type:
- apiref
ms.openlocfilehash: 835b01e1c808c071e9393c5117d5e38415ec8eba
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728621"
---
# <a name="iclrtask2-interface"></a>Interface ICLRTask2

Fornece toda a funcionalidade da interface [ICLRTask](iclrtask-interface.md) ; Além disso, o fornece métodos que permitem que as anulações de thread sejam atrasadas no thread atual.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método BeginPreventAsyncAbort](iclrtask2-beginpreventasyncabort-method.md)|Atrasa novas solicitações de anulação de thread no thread atual.|  
|[Método EndPreventAsyncAbort](iclrtask2-endpreventasyncabort-method.md)|Permite solicitações de anulação de thread novas ou pendentes para resultar em anulações de thread no thread atual.|  
  
## <a name="remarks"></a>Comentários  

 A `ICLRTask2` interface herda a `ICLRTask` interface e adiciona métodos que permitem ao host atrasar anulações de thread, proteger uma região de código que não deve falhar. Chamar `BeginPreventAsyncAbort` incrementa o contador atraso-thread-Abort para o thread atual e chamá `EndPreventAsyncAbort` -lo o decrementa. Chamadas para `BeginPreventAsyncAbort` e `EndPreventAsyncAbort` podem ser aninhadas. Desde que o contador seja maior que zero, as anulações de thread para o thread atual serão atrasadas.  
  
 Se chamadas para `BeginPreventAsyncAbort` e `EndPreventAsyncAbort` não são emparelhadas, é possível alcançar um estado no qual as anulações de thread não podem ser entregues ao thread atual.  
  
 O atraso não é respeitado para um thread que se anula.  
  
 A funcionalidade exposta por esse recurso é usada internamente pela VM (máquina virtual). O uso indevido desses métodos pode causar um comportamento não especificado na VM. Por exemplo, chamar `EndPreventAsyncAbort` sem primeiro chamar `BeginPreventAsyncAbort` pode definir o contador como zero quando a VM o tiver aumentado anteriormente. Da mesma forma, o contador interno não é verificado quanto ao estouro. Se ele exceder seu limite integral porque é incrementado pelo host e pela VM, o comportamento resultante não é especificado.  
  
 Para obter informações sobre membros herdados de `ICLRTask` e sobre outros usos dessa interface, consulte a interface [ICLRTask](iclrtask-interface.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRTask](iclrtask-interface.md)
- [Interface ICLRTaskManager](iclrtaskmanager-interface.md)
- [Interface IHostTask](ihosttask-interface.md)
- [Interface IHostTaskManager](ihosttaskmanager-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
