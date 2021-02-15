---
description: 'Saiba mais sobre: enumeração EApiCategories'
title: Enumeração EApiCategories
ms.date: 03/30/2017
api_name:
- EApiCategories
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EApiCategories
helpviewer_keywords:
- EApiCategories enumeration [.NET Framework hosting]
ms.assetid: 3c4a8a5a-8a46-4ac9-947f-4959bc9d6ac6
topic_type:
- apiref
ms.openlocfilehash: 58a7d4fa4d0c965bf9158ad6713185782d4ae94a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785621"
---
# <a name="eapicategories-enumeration"></a>Enumeração EApiCategories

Descreve as categorias de recursos que o host pode bloquear de ser executado em código parcialmente confiável.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    eNoCategory               = 0,  
    eSynchronization          = 0x1,  
    eSharedState              = 0x2,  
    eExternalProcessMgmt      = 0x4,  
    eSelfAffectingProcessMgmt = 0x8,  
    eExternalThreading        = 0x10,  
    eSelfAffectingThreading   = 0x20,  
    eSecurityInfrastructure   = 0x40,  
    eUI                       = 0x80,  
    eMayLeakOnAbort           = 0x100,  
    eAll                      = 0x1ff  
} EHostProtectionCategories;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`eAll`|Especifica que todas as classes gerenciadas e membros cobertos por outros `EApiCategories` campos sejam impedidos de serem executados em código parcialmente confiável.|  
|`eExternalProcessMgmt`|Especifica que classes e membros gerenciados que permitem a criação, manipulação e destruição de processos externos sejam impedidos de serem executados em código parcialmente confiável.|  
|`eExternalThreading`|Especifica que classes e membros gerenciados que permitem a criação, manipulação e destruição de threads externos sejam impedidos de serem executados em código parcialmente confiável.|  
|`eMayLeakOnAbort`|Especifica que os tipos gerenciados e membros que poderiam vazar memória em anulação sejam impedidos de serem executados em código parcialmente confiável.|  
|`eNoCategory`|Especifica que nenhuma categoria de código gerenciado será impedida de ser executada em código parcialmente confiável.|  
|`eSecurityInfrastructure`|Especifica que a infraestrutura de segurança Common Language Runtime (CLR) seja impedida de ser usada pelo código parcialmente confiável.|  
|`eSelfAffectingProcessMgmt`|Especifica que classes e membros gerenciados cujos recursos podem afetar o processo hospedado sejam impedidos de serem executados em código parcialmente confiável.|  
|`eSelfAffectingThreading`|Especifica que classes e membros gerenciados cujos recursos podem afetar threads no processo hospedado serão impedidos de serem executados em código parcialmente confiável.|  
|`eSharedState`|Especifica que classes e membros gerenciados que expõem o estado compartilhado sejam impedidos de serem executados em código parcialmente confiável.|  
|`eSynchronization`|Especifica que Common Language Runtime classes e membros que permitem que o código do usuário mantenha bloqueios sejam impedidos de serem executados em código parcialmente confiável.|  
|`eUI`|Especifica que classes e membros gerenciados que permitem ou exigem interação humana são impedidos de serem executados em código parcialmente confiável.|  
  
## <a name="remarks"></a>Comentários  

 O método [ICLRHostProtectionManager:: SetProtectedCategories](iclrhostprotectionmanager-setprotectedcategories-method.md) usa um parâmetro do tipo `EApiCategories` .  
  
 A `EApiCategories` enumeração e o `SetProtectedCategories` método estão diretamente relacionados à classe gerenciada <xref:System.Security.Permissions.HostProtectionAttribute?displayProperty=nameWithType> . A classe gerenciada é usada com a <xref:System.Security.Permissions.HostProtectionResource?displayProperty=nameWithType> Enumeração cujos valores correspondem diretamente aos `EApiCategories` valores, para marcar tipos gerenciados e membros que expõem recursos correspondentes às categorias descritas por `EApiCategories` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRHostProtectionManager](iclrhostprotectionmanager-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
