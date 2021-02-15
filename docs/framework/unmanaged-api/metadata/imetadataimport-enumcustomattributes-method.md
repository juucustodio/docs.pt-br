---
description: 'Saiba mais sobre o método: IMetaDataImport:: EnumCustomAttributes'
title: Método IMetaDataImport::EnumCustomAttributes
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumCustomAttributes
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumCustomAttributes
helpviewer_keywords:
- EnumCustomAttributes method [.NET Framework metadata]
- IMetaDataImport::EnumCustomAttributes method [.NET Framework metadata]
ms.assetid: 798513a0-68b1-4d04-bc5b-782a4445ea68
topic_type:
- apiref
ms.openlocfilehash: 1c55ea4b72483e5dc30425172b95be7f77e8a62a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99677581"
---
# <a name="imetadataimportenumcustomattributes-method"></a>Método IMetaDataImport::EnumCustomAttributes

Enumera os tokens de definição de atributo personalizados associados ao tipo ou membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumCustomAttributes (
   [in, out] HCORENUM      *phEnum,  
   [in]  mdToken            tk,
   [in]  mdToken            tkType,
   [out] mdCustomAttribute  rCustomAttributes[],
   [in]  ULONG              cMax,  
   [out, optional] ULONG   *pcCustomAttributes  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `phEnum`  
 [entrada, saída] Um ponteiro para o enumerador retornado.  
  
 `tk`  
 no Um token para o escopo da enumeração ou zero para todos os atributos personalizados.  
  
 `tkType`  
 no Um token para o construtor do tipo dos atributos a serem enumerados ou `null` para todos os tipos.  
  
 `rCustomAttributes`  
 fora Uma matriz de tokens de atributo personalizados.  
  
 `cMax`  
 no O tamanho máximo da `rCustomAttributes` matriz.  
  
 `pcCustomAttributes`  
 [saída, opcional] O número real de valores de token retornados em `rCustomAttributes` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|`S_OK`|`EnumCustomAttributes` retornado com êxito.|  
|`S_FALSE`|Não há atributos personalizados para enumerar. Nesse caso, `pcCustomAttributes` é zero.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
