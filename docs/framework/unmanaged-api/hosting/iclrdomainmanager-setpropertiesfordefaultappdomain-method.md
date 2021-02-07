---
description: 'Saiba mais sobre o método: ICLRDomainManager:: SetPropertiesForDefaultAppDomain'
title: Método ICLRDomainManager::SetPropertiesForDefaultAppDomain
ms.date: 03/30/2017
api_name:
- ICLRDomainManager.SetPropertiesForDefaultAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager::SetPropertiesForDefaultAppDomain
helpviewer_keywords:
- ICLRDomainManager::SetPropertiesForDefaultAppDomain method [.NET Framework hosting]
- SetPropertiesForDefaultAppDomain method [.NET Framework hosting]
ms.assetid: 43e61c4b-c435-45ec-9ef6-c68403aa4200
ms.openlocfilehash: 08e6c885d5d089fa22c30a4e3cef69480b840031
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689437"
---
# <a name="iclrdomainmanagersetpropertiesfordefaultappdomain-method"></a>Método ICLRDomainManager::SetPropertiesForDefaultAppDomain

Define as propriedades que serão usadas para inicializar o domínio de aplicativo padrão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetPropertiesForDefaultAppDomain(  
    [in] DWORD nProperties,  
    [in] LPCWSTR *pwszPropertyNames,  
    [in] LPCWSTR *pwszPropertyValues  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `nProperties`  
 no O número de entradas no `pwszPropertyNames` e no `pwszPropertyValues` .  
  
 `pwszPropertyNames`  
 no Uma matriz de nomes de propriedade ou NULL se não houver propriedades. Atualmente, o único nome de propriedade reconhecido por esse método é "PARTIAL_TRUST_VISIBLE_ASSEMBLIES".  
  
 `pwszPropertyValues`  
 no Uma matriz de valores de propriedade ou NULL se não houver nenhuma propriedade.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|HRESULT_FROM_WIN32 (ERROR_UNKNOWN_PROPERTY)|`pwszPropertyNames` inclui um nome de propriedade que não é reconhecido por este método.|  
  
## <a name="remarks"></a>Comentários  

 O valor da propriedade para "PARTIAL_TRUST_VISIBLE_ASSEMBLIES" é uma lista de ASSEMBLIES que têm o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo condicional (APTCA) com o <xref:System.Security.PartialTrustVisibilityLevel.NotVisibleByDefault?displayProperty=nameWithType> sinalizador, que deve se tornar visível para chamadores parcialmente confiáveis no domínio do aplicativo padrão.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Hospedagem](index.md)
- [Interface ICLRDomainManager](iclrdomainmanager-interface.md)
