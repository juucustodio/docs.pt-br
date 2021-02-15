---
description: 'Saiba mais sobre: IMetaDataEmit: método efineProperty de:D'
title: Método IMetaDataEmit::DefineProperty
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineProperty
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineProperty
helpviewer_keywords:
- IMetaDataEmit::DefineProperty method [.NET Framework metadata]
- DefineProperty method [.NET Framework metadata]
ms.assetid: 5c4c1dc2-d40d-4173-bbe6-7058fb21c98f
topic_type:
- apiref
ms.openlocfilehash: c0c0b6009f8674a5edebf1c982e277f4ca5b185b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784022"
---
# <a name="imetadataemitdefineproperty-method"></a>Método IMetaDataEmit::DefineProperty

Cria uma definição de propriedade para o tipo especificado, com os `get` `set` acessadores de método e especificados, e Obtém um token para essa definição de propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineProperty (
    [in]  mdTypeDef          td,
    [in]  LPCWSTR            szProperty,
    [in]  DWORD              dwPropFlags,
    [in]  PCCOR_SIGNATURE    pvSig,
    [in]  ULONG              cbSig,
    [in]  DWORD              dwCPlusTypeFlag,
    [in]  void const         *pValue,
    [in]  ULONG              cchValue,
    [in]  mdMethodDef        mdSetter,
    [in]  mdMethodDef        mdGetter,
    [in]  mdMethodDef        rmdOtherMethods[],
    [out] mdProperty         *pmdProp
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `td`  
 no O token para a classe ou interface na qual a propriedade está sendo definida.  
  
 `szProperty`  
 no O nome da propriedade.  
  
 `dwPropFlags`  
 no Os sinalizadores de propriedade.  
  
 `pvSig`  
 no A assinatura da propriedade.  
  
 `cbSig`  
 no A contagem de bytes em `pvSig` .  
  
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
 no Uma matriz de outros métodos associados à propriedade. Encerre a matriz com um `mdTokenNil` .  
  
 `pmdProp`  
 fora O `mdProperty` token atribuído.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
