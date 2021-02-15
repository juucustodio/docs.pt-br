---
description: 'Saiba mais sobre: Enumeração EInitializeNewDomainFlags'
title: Enumeração EInitializeNewDomainFlags
ms.date: 03/30/2017
api_name:
- EInitializeNewDomainFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EInitializeNewDomainFlags
helpviewer_keywords:
- EInitializeNewDomainFlags enumeration [.NET Framework hosting]
ms.assetid: 3a120ab2-f5ef-4c9b-8595-d3ed7247c342
ms.openlocfilehash: b856d061e86c0c79b35f842975378307b79a37e7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785458"
---
# <a name="einitializenewdomainflags-enumeration"></a>Enumeração EInitializeNewDomainFlags

Permite que o host forneça o tempo de execução com informações sobre a inicialização de um domínio de aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    eInitializeNewDomainFlags_None              = 0x0000,  
    eInitializeNewDomainFlags_NoSecurityChanges = 0x0002  
} EInitializeNewDomainFlags;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`eInitializeNewDomainFlags_None`|Sem sinalizadores.|  
|`eInitializeNewDomainFlags_NoSecurityChanges`|Informa ao Common Language Runtime (CLR) que o host não fará alterações no estado de segurança do domínio do aplicativo no <xref:System.AppDomainManager.InitializeNewDomain%2A> método.|  
  
## <a name="remarks"></a>Comentários  

 O método [ICLRDomainManager:: SetAppDomainManagerType](iclrdomainmanager-setappdomainmanagertype-method.md) usa um parâmetro do tipo `EInitializeNewDomainFlags` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Hospedando enumerações](hosting-enumerations.md)
- [Método SetAppDomainManagerType](iclrdomainmanager-setappdomainmanagertype-method.md)
