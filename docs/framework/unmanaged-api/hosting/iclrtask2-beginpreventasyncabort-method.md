---
description: 'Saiba mais sobre o método: ICLRTask2:: BeginPreventAsyncAbort'
title: Método ICLRTask2::BeginPreventAsyncAbort
ms.date: 03/30/2017
api_name:
- ICLRTask2.BeginPreventAsyncAbort
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2::BeginPreventAsyncAbort
helpviewer_keywords:
- ICLRTask2::BeginPreventAsyncAbort method [.NET Framework hosting]
- BeginPreventAsyncAbort method [.NET Framework hosting]
ms.assetid: 75754c2f-38c7-4707-85fe-559db4542729
topic_type:
- apiref
ms.openlocfilehash: 1e25cb0e6157d77efc6a04016dc49d9d5d0bf116
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728620"
---
# <a name="iclrtask2beginpreventasyncabort-method"></a>Método ICLRTask2::BeginPreventAsyncAbort

Atrasa novas solicitações de anulação de threads resultando em anulações de thread no thread atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT BeginPreventAsyncAbort();  
```  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|HOST_E_INVALIDOPERATION|O método foi chamado em um thread que não é o thread atual.|  
  
## <a name="remarks"></a>Comentários  

 Chamar esse método incrementa o contador atraso-thread-anulação para o thread atual por um.  
  
 Chamadas para `BeginPreventAsyncAbort` e [ICLRTask2:: EndPreventAsyncAbort](iclrtask2-endpreventasyncabort-method.md) podem ser aninhadas. Desde que o contador seja maior que zero, as anulações de thread para o thread atual serão atrasadas. Se essa chamada não for emparelhada com uma chamada para o `EndPreventAsyncAbort` método, é possível alcançar um estado no qual as anulações de thread não podem ser entregues ao thread atual.  
  
 O atraso não é respeitado para um thread que se anula.  
  
 A funcionalidade exposta por esse recurso é usada internamente pela VM (máquina virtual). O uso indevido desses métodos pode causar um comportamento não especificado na VM. Por exemplo, chamar `EndPreventAsyncAbort` sem primeiro chamar `BeginPreventAsyncAbort` pode definir o contador como zero quando a VM o tiver aumentado anteriormente. Da mesma forma, o contador interno não é verificado quanto ao estouro. Se ele exceder seu limite integral porque é incrementado pelo host e pela VM, o comportamento resultante não é especificado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método EndPreventAsyncAbort](iclrtask2-endpreventasyncabort-method.md)
- [Interface ICLRTask2](iclrtask2-interface.md)
- [Interface ICLRTaskManager](iclrtaskmanager-interface.md)
- [Interface IHostTask](ihosttask-interface.md)
- [Interface IHostTaskManager](ihosttaskmanager-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
