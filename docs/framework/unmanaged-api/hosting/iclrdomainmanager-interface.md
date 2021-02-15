---
description: 'Saiba mais sobre: interface ICLRDomainManager'
title: Interface ICLRDomainManager
ms.date: 03/30/2017
api_name:
- ICLRDomainManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager
helpviewer_keywords:
- ICLRDomainManager interface [.NET Framework hosting]
ms.assetid: f08b2390-d872-4521-a815-e9c237c4c45d
ms.openlocfilehash: d719e89d81e8c7abb1f238ce50b4e236de17ac72
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790003"
---
# <a name="iclrdomainmanager-interface"></a>Interface ICLRDomainManager

Permite que o host especifique o Gerenciador de domínio de aplicativo que será usado para inicializar o domínio de aplicativo padrão e para especificar as propriedades de inicialização.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método SetAppDomainManagerType](iclrdomainmanager-setappdomainmanagertype-method.md)|Especifica o tipo, derivado da <xref:System.AppDomainManager?displayProperty=nameWithType> classe, do Gerenciador de domínio de aplicativo que será usado para inicializar o domínio de aplicativo padrão.|  
|[Método SetPropertiesForDefaultAppDomain](iclrdomainmanager-setpropertiesfordefaultappdomain-method.md)|Define as propriedades que serão usadas para inicializar o domínio de aplicativo padrão.|  
  
## <a name="remarks"></a>Comentários  

 Para obter uma instância dessa interface, chame o método [ICLRControl:: GetCLRManager](iclrcontrol-getclrmanager-method.md) com o tipo de Gerenciador IID `IID_ICLRDomainManager` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
