---
description: 'Saiba mais sobre: IMetaDataEmit: método efineTypeDef de:D'
title: Método IMetaDataEmit::DefineTypeDef
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineTypeDef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineTypeDef
helpviewer_keywords:
- IMetaDataEmit::DefineTypeDef method [.NET Framework metadata]
- DefineTypeDef method [.NET Framework metadata]
ms.assetid: dd11c485-be95-4b97-9cd8-68679a4fb432
topic_type:
- apiref
ms.openlocfilehash: ca0c74b8c067771e9f45a8c00639d75c9ad08de1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784027"
---
# <a name="imetadataemitdefinetypedef-method"></a>Método IMetaDataEmit::DefineTypeDef

Cria uma definição de tipo para um tipo de Common Language Runtime e Obtém um token de metadados para essa definição de tipo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineTypeDef (
    [in]  LPCWSTR     szTypeDef,
    [in]  DWORD       dwTypeDefFlags,
    [in]  mdToken     tkExtends,
    [in]  mdToken     rtkImplements[],
    [out] mdTypeDef   *ptd  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szTypeDef`  
 no O nome do tipo em Unicode.  
  
 `dwTypeDefFlags`  
 [in] `TypeDef` atributos. Esta é uma bitmask de `CoreTypeAttr` valores.  
  
 `tkExtends`  
 no O token da classe base. Ele deve ser um `mdTypeDef` ou um `mdTypeRef` token.  
  
 `rtkImplements`  
 no Uma matriz de tokens que especifica as interfaces que essa classe ou interface implementa.  
  
 `ptd`  
 fora O `mdTypeDef` token atribuído.  
  
## <a name="remarks"></a>Comentários  

 Um sinalizador em `dwTypeDefFlags` especifica se o tipo que está sendo criado é um tipo de referência de Common Type System (classe ou interface) ou um tipo de valor de Common Type System.  
  
 Dependendo dos parâmetros fornecidos, esse método, como um efeito colateral, também pode criar um `mdInterfaceImpl` registro para cada interface herdada ou implementada por esse tipo. No entanto, esse método não retorna nenhum desses `mdInterfaceImpl` tokens. Se um cliente quiser adicionar ou modificar um token posteriormente `mdInterfaceImpl` , ele deverá usar a `IMetaDataImport` interface para enumerá-los. Se você quiser usar a semântica COM da `[default]` interface, deverá fornecer a interface padrão como o primeiro elemento em `rtkImplements` ; um atributo personalizado definido na classe indicará que a classe tem uma interface padrão (que sempre é considerada o primeiro `mdInterfaceImpl` token declarado para a classe).  
  
 Cada elemento da `rtkImplements` matriz contém um `mdTypeDef` token ou `mdTypeRef` . O último elemento na matriz deve ser `mdTokenNil` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
