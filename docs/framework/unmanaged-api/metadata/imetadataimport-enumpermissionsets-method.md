---
description: 'Saiba mais sobre o método: IMetaDataImport:: EnumPermissionSets'
title: Método IMetaDataImport::EnumPermissionSets
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumPermissionSets
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumPermissionSets
helpviewer_keywords:
- EnumPermissionSets method [.NET Framework metadata]
- IMetaDataImport::EnumPermissionSets method [.NET Framework metadata]
ms.assetid: 347d7e5c-c90f-45ad-bd1e-2c7912b0b19c
topic_type:
- apiref
ms.openlocfilehash: 7138cb2a89ecbea1afbf3e9fccfcac26e7e0fd7a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99688748"
---
# <a name="imetadataimportenumpermissionsets-method"></a>Método IMetaDataImport::EnumPermissionSets

Enumera permissões para os objetos em um escopo de metadados especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumPermissionSets  
   [in, out] HCORENUM      *phEnum,
   [in]      mdToken       tk,
   [in]      DWORD         dwActions,  
   [out]     mdPermission  rPermission[],  
   [in]      ULONG         cMax,  
   [out]     ULONG         *pcTokens  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `phEnum`  
 [entrada, saída] Um ponteiro para o enumerador. Isso deve ser nulo para a primeira chamada deste método.  
  
 `tk`  
 no Um token de metadados que limita o escopo da pesquisa ou nulo para pesquisar o escopo mais amplo possível.  
  
 `dwActions`  
 no Sinalizadores que representam os <xref:System.Security.Permissions.SecurityAction> valores a serem incluídos `rPermission` ou zero para retornar todas as ações.  
  
 `rPermission`  
 fora A matriz usada para armazenar os tokens de permissão.  
  
 `cMax`  
 no O tamanho máximo da `rPermission` matriz.  
  
 `pcTokens`  
 fora O número de tokens de permissão retornados em `rPermission` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|`S_OK`|`EnumPermissionSets` retornado com êxito.|  
|`S_FALSE`|Não há tokens para enumerar. Nesse caso, `pcTokens` é zero.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
