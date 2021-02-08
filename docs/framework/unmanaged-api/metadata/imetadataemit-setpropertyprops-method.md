---
description: 'Saiba mais sobre o método: IMetaDataEmit:: SetPropertyProps'
title: Método IMetaDataEmit::SetPropertyProps
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetPropertyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetPropertyProps
helpviewer_keywords:
- SetPropertyProps method [.NET Framework metadata]
- IMetaDataEmit::SetPropertyProps method [.NET Framework metadata]
ms.assetid: e2501fc8-b2bc-4dcc-9205-e3acd5a53ffe
topic_type:
- apiref
ms.openlocfilehash: ad5efa86b4f774bcaa2251cb992c2dd52ac28bdd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99771828"
---
# <a name="imetadataemitsetpropertyprops-method"></a>Método IMetaDataEmit::SetPropertyProps

Define os recursos armazenados em metadados para uma propriedade definida por uma chamada anterior para o [método definoproperty](imetadataemit-defineproperty-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetPropertyProps (
    [in]  mdProperty      pr,
    [in]  DWORD           dwPropFlags,
    [in]  DWORD           dwCPlusTypeFlag,
    [in]  void const      *pValue,
    [in]  ULONG           cchValue,
    [in]  mdMethodDef     mdSetter,
    [in]  mdMethodDef     mdGetter,
    [in]  mdMethodDef     rmdOtherMethods[]
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pr`  
 no O token para a propriedade a ser alterada  
  
 `dwPropFlags`  
 no Sinalizadores de propriedade.  
  
 `dwCPlusTypeFlag`  
 no O tipo do valor padrão da propriedade.  
  
 `pValue`  
 no O valor padrão para a propriedade.  
  
 `cchValue`  
 no A contagem de caracteres (Unicode) no `pValue` .  
  
 `mdSetter`  
 no O método que define o valor da propriedade.  
  
 `mdGetter`  
 no O método que obtém o valor da propriedade.  
  
 `rmdOtherMethods[]`  
 no Uma matriz de outros métodos associados à propriedade. Terminar esta matriz com um `mdTokenNil` token.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
