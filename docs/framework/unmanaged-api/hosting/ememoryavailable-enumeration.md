---
description: 'Saiba mais sobre: Enumeração EMemoryAvailable'
title: Enumeração EMemoryAvailable
ms.date: 03/30/2017
api_name:
- EMemoryAvailable
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EMemoryAvailable
helpviewer_keywords:
- EMemoryAvailable enumeration [.NET Framework hosting]
ms.assetid: 38e72a06-dbed-473b-a59b-7e0b3ea4f2af
topic_type:
- apiref
ms.openlocfilehash: fdb33b45c354d39b1a52fd815a44041b659181ec
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785439"
---
# <a name="ememoryavailable-enumeration"></a>Enumeração EMemoryAvailable

Contém valores que indicam a quantidade de memória física livre no computador. Esses valores são mapeados logicamente para os eventos de memória alta e baixa retornada da `CreateMemoryResourceNotification` função na API do Windows.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    eMemoryAvailableLow     = 1,  
    eMemoryAvailableNeutral = 2,  
    eMemoryAvailableHigh    = 3
} EMemoryAvailable;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`eMemoryAvailableHigh`|Há muita memória física disponível.|  
|`eMemoryAvailableLow`|Há pouca memória física disponível.|  
|`eMemoryAvailableNeutral`|A memória física disponível é neutra.|  
  
## <a name="remarks"></a>Comentários  

 Esse valor é passado pelo host para o Common Language Runtime (CLR) usando uma chamada para o método [ICLRMemoryNotificationCallback:: OnMemoryNotification](iclrmemorynotificationcallback-onmemorynotification-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Hospedando enumerações](hosting-enumerations.md)
