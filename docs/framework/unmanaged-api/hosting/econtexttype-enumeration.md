---
description: 'Saiba mais sobre: Enumeração EContextType'
title: Enumeração EContextType
ms.date: 03/30/2017
api_name:
- EContextType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EContextType
helpviewer_keywords:
- EContextType enumeration [.NET Framework hosting]
ms.assetid: 92b926a9-b87e-408a-9036-df7b752c9492
topic_type:
- apiref
ms.openlocfilehash: b7d6ddb385386bb0616a01ef6fcc432f2c925d51
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785520"
---
# <a name="econtexttype-enumeration"></a>Enumeração EContextType

Descreve o contexto de segurança do thread em execução no momento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    eCurrentContext    = 0x00,  
    eRestrictedContext = 0x01  
} EContextType;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`eCurrentContext`|Indica o contexto no thread atual no momento em que o Common Language Runtime (CLR) chama o método [IHostSecurityManager:: GetSecurityContext](ihostsecuritymanager-getsecuritycontext-method.md) ou o contexto solicitado pelo CLR em uma chamada para o método [IHostSecurityManager:: SetSecurityContext](ihostsecuritymanager-setsecuritycontext-method.md) .|  
|`eRestrictedContext`|Indica um contexto sobre o qual o host tem privilégios mais baixos, como o coletor de lixo ou construtores de classe ou módulo.|  
  
## <a name="remarks"></a>Comentários  

 O CLR fornece um dos `EContextType` valores como um valor de parâmetro em chamadas para os `IHostSecurityManager::GetSecurityContext` `IHostSecurityManager::SetSecurityContext` métodos e.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostSecurityContext](ihostsecuritycontext-interface.md)
- [Interface IHostSecurityManager](ihostsecuritymanager-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
