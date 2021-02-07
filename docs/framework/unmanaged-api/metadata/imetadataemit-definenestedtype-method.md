---
description: 'Saiba mais sobre: IMetaDataEmit: método efineNestedType de:D'
title: Método IMetaDataEmit::DefineNestedType
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineNestedType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineNestedType
helpviewer_keywords:
- IMetaDataEmit::DefineNestedType method [.NET Framework metadata]
- DefineNestedType method [.NET Framework metadata]
ms.assetid: 1e994de6-4628-459c-b967-b34be1e9fe4f
topic_type:
- apiref
ms.openlocfilehash: 1b0c5c8d1bffa425b2019a4434042c84a0069907
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753374"
---
# <a name="imetadataemitdefinenestedtype-method"></a>Método IMetaDataEmit::DefineNestedType

Cria a assinatura de metadados de uma definição de tipo, retorna um `mdTypeDef` token para esse tipo e especifica que o tipo definido é um membro do tipo referenciado pelo `tdEncloser` parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineNestedType (
    [in]  LPCWSTR     szTypeDef,  
    [in]  DWORD       dwTypeDefFlags,
    [in]  mdToken     tkExtends,
    [in]  mdToken     rtkImplements[],
    [in]  mdTypeDef   tdEncloser,
    [out] mdTypeDef   *ptd  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szTypeDef`  
 no O nome do tipo em Unicode.  
  
 `dwTypeDefFlags`  
 [in] `TypeDef` atributos. Esta é uma bitmask de `CorTypeAttr` valores.  
  
 `tkExtends`  
 no O token da classe base. Este é um `mdTypeDef` `mdTypeRef` token ou.  
  
 `rtkImplements`[]  
 no Uma matriz de tokens que especificam as interfaces que essa classe ou interface implementa.  
  
 `tdEncloser`  
 no O token do tipo delimitador. O último elemento da matriz deve ser `mdTokenNil` .  
  
 `ptd`  
 fora O `mdTypeDef` token atribuído.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
