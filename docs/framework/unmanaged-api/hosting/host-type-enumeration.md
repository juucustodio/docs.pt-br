---
description: 'Saiba mais sobre: enumeração de HOST_TYPE'
title: Enumeração HOST_TYPE
ms.date: 03/30/2017
api_name:
- HOST_TYPE
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- HOST_TYPE
helpviewer_keywords:
- HOST_TYPE enumeration [.NET Framework hosting]
ms.assetid: 51f848be-84c5-4036-9839-c762c576bbf5
topic_type:
- apiref
ms.openlocfilehash: 6a0baf3050f99885953ddec06342cbe19accfef3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785231"
---
# <a name="host_type-enumeration"></a>Enumeração HOST_TYPE

Contém valores que especificam o tipo de host que está iniciando um aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    HOST_TYPE_DEFAULT     = 0x0,  
    HOST_TYPE_APPLAUNCH   = 0x1,  
    HOST_TYPE_CORFLAG     = 0x2  
} HOST_TYPE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`HOST_TYPE_APPLAUNCH`|Inicie o aplicativo a partir de AppLaunch.exe.<br /><br /> Use esse valor para aplicativos parcialmente confiáveis.|  
|`HOST_TYPE_CORFLAG`|Inicie o aplicativo diretamente. Ou seja, inicie o aplicativo a partir de seu próprio arquivo. exe.<br /><br /> Use esse valor para aplicativos totalmente confiáveis.|  
|`HOST_TYPE_DEFAULT`|O mesmo que HOST_TYPE_APPLAUNCH.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Hospedando enumerações](hosting-enumerations.md)
