---
description: 'Saiba mais sobre: interface ICLRAssemblyReferenceList'
title: Interface ICLRAssemblyReferenceList
ms.date: 03/30/2017
api_name:
- ICLRAssemblyReferenceList
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyReferenceList
helpviewer_keywords:
- ICLRAssemblyReferenceList interface [.NET Framework hosting]
ms.assetid: 5f890fdf-d22a-429e-a35f-135273d1a636
topic_type:
- apiref
ms.openlocfilehash: f5ef4efd343ebc18c443482f4697a3d299c5aac1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716777"
---
# <a name="iclrassemblyreferencelist-interface"></a>Interface ICLRAssemblyReferenceList

Gerencia uma lista de assemblies que são carregados pelo Common Language Runtime (CLR) e não pelo host.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método IsAssemblyReferenceInList](iclrassemblyreferencelist-isassemblyreferenceinlist-method.md)|Obtém um valor que indica se o ponteiro fornecido faz referência a um assembly na lista.|  
|[Método IsStringAssemblyReferenceInList](iclrassemblyreferencelist-isstringassemblyreferenceinlist-method.md)|Obtém um valor que indica se o nome fornecido corresponde ao nome de um assembly na lista.|  
  
## <a name="remarks"></a>Comentários  

 Chame o método [ICLRAssemblyIdentityManager:: GetCLRAssemblyReferenceList](iclrassemblyidentitymanager-getclrassemblyreferencelist-method.md) para obter um ponteiro para uma instância do `ICLRAssemblyReferenceList` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md)
- [Interface IHostAssemblyStore](ihostassemblystore-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
