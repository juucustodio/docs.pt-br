---
description: 'Saiba mais sobre: interface ICLRMemoryNotificationCallback'
title: Interface ICLRMemoryNotificationCallback
ms.date: 03/30/2017
api_name:
- ICLRMemoryNotificationCallback
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMemoryNotificationCallback
helpviewer_keywords:
- ICLRMemoryNotificationCallback interface [.NET Framework hosting]
ms.assetid: 873639e2-4837-4568-83b3-4493e67e4174
topic_type:
- apiref
ms.openlocfilehash: 46e53cdf0b7f797b8945237d47fc3b521b08ddb7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689216"
---
# <a name="iclrmemorynotificationcallback-interface"></a>Interface ICLRMemoryNotificationCallback

Permite que o host relate condições de pressão de memória usando uma abordagem semelhante à da `CreateMemoryResourceNotification` função do Win32.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método OnMemoryNotification](iclrmemorynotificationcallback-onmemorynotification-method.md)|Notifica o Common Language Runtime (CLR) da carga de memória no computador.|  
  
## <a name="remarks"></a>Comentários  

 O host usa a `ICLRMemoryNotificationCallback` interface para solicitar que os recursos de memória livre do CLR.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostMemoryManager](ihostmemorymanager-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
