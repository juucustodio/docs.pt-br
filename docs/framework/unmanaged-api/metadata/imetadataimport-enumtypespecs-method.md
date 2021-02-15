---
description: 'Saiba mais sobre o método: IMetaDataImport:: EnumTypeSpecs'
title: Método IMetaDataImport::EnumTypeSpecs
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumTypeSpecs
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumTypeSpecs
helpviewer_keywords:
- EnumTypeSpecs method [.NET Framework metadata]
- IMetaDataImport::EnumTypeSpecs method [.NET Framework metadata]
ms.assetid: 75331c7b-988b-436c-9eb9-a270d37b4f06
topic_type:
- apiref
ms.openlocfilehash: 7446bbf3296ffb6cfa3a20f594b4a7da22acff5c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799337"
---
# <a name="imetadataimportenumtypespecs-method"></a>Método IMetaDataImport::EnumTypeSpecs

Enumera os tokens de TypeSpec definidos no escopo de metadados atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumTypeSpecs (  
   [in, out] HCORENUM    *phEnum,  
   [out] mdTypeSpec      rTypeSpecs[],  
   [in]  ULONG           cMax,  
   [out] ULONG           *pcTypeSpecs  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `phEnum`  
 [entrada, saída] Um ponteiro para o enumerador. Esse valor deve ser nulo para a primeira chamada deste método.  
  
 `rTypeSpecs`  
 fora A matriz usada para armazenar os tokens de TypeSpec.  
  
 `cMax`  
 no O tamanho máximo da `rTypeSpecs` matriz.  
  
 `pcTypeSpecs`  
 fora O número de tokens TypeSpec retornados em `rTypeSpecs` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|`S_OK`|`EnumTypeSpecs` retornado com êxito.|  
|`S_FALSE`|Não há tokens para enumerar. Nesse caso, `pcTypeSpecs` é zero.|  
  
## <a name="remarks"></a>Comentários  

 Os tokens TypeSpec são criados pelo método [IMetaDataEmit:: GetTokenFromTypeSpec](imetadataemit-gettokenfromtypespec-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
