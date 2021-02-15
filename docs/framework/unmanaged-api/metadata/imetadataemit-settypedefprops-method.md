---
description: 'Saiba mais sobre o método: IMetaDataEmit:: SetTypeDefProps'
title: Método IMetaDataEmit::SetTypeDefProps
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetTypeDefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetTypeDefProps
helpviewer_keywords:
- SetTypeDefProps method [.NET Framework metadata]
- IMetaDataEmit::SetTypeDefProps method [.NET Framework metadata]
ms.assetid: 480d596a-759f-4d29-ac1a-3dbff8f3544d
topic_type:
- apiref
ms.openlocfilehash: 1160d20e7ceb422390f8cd725a75fdb4f42318e7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99706494"
---
# <a name="imetadataemitsettypedefprops-method"></a>Método IMetaDataEmit::SetTypeDefProps

Define recursos de um tipo definido por uma chamada anterior para [IMetaDataEmit::D efinetypedef](imetadataemit-definetypedef-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetTypeDefProps (  
    [in]  mdTypeDef   td,
    [in]  DWORD       dwTypeDefFlags,
    [in]  mdToken     tkExtends,
    [in]  mdToken     rtkImplements[]
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `td`  
 no Um `mdTypeDef` token obtido da chamada original para [IMetaDataEmit::D efinetypedef](imetadataemit-definetypedef-method.md).  
  
 `dwTypeDefFlags`  
 [in] `TypeDef` atributos. Esta é uma bitmask de `CorTypeAttr` valores.  
  
 `tkExtends`  
 no O `mdToken` da classe base. Obtido de uma chamada anterior para [IMetaDataEmit::D efineimporttype](imetadataemit-defineimporttype-method.md)ou `null` .  
  
 `rtkImplements[]`  
 no Uma matriz de tokens para as interfaces que esse tipo implementa. Esses `mdTypeRef` tokens são obtidos usando [IMetaDataEmit::D efineimporttype](imetadataemit-defineimporttype-method.md). O último elemento da matriz deve ser `mdTokenNil` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
