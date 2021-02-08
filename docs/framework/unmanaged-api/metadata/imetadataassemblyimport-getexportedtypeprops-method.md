---
description: 'Saiba mais sobre o método: IMetaDataAssemblyImport:: GetExportedTypeProps'
title: Método IMetaDataAssemblyImport::GetExportedTypeProps
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetExportedTypeProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetExportedTypeProps
helpviewer_keywords:
- GetExportedTypeProps method [.NET Framework metadata]
- IMetaDataAssemblyImport::GetExportedTypeProps method [.NET Framework metadata]
ms.assetid: 25ca7623-5a55-4f09-b44a-36b03d142278
topic_type:
- apiref
ms.openlocfilehash: 894fb65fb6de76a218489b2a85a2d3c20c572789
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784113"
---
# <a name="imetadataassemblyimportgetexportedtypeprops-method"></a>Método IMetaDataAssemblyImport::GetExportedTypeProps

Obtém o conjunto de propriedades do tipo exportado com a assinatura de metadados especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetExportedTypeProps (  
    [in]  mdExportedType    mdct,
    [out] LPWSTR            szName,
    [in]  ULONG             cchName,
    [out] ULONG             *pchName,
    [out] mdToken           *ptkImplementation,
    [out] mdTypeDef         *ptkTypeDef,
    [out] DWORD             *pdwExportedTypeFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `mdct`  
 no Um `mdExportedType` token de metadados que representa o tipo exportado.  
  
 `szName`  
 fora O nome do tipo exportado.  
  
 `cchName`  
 no O tamanho, em caracteres largos, de `szName` .  
  
 `pchName`  
 fora O número de caracteres largos realmente retornados em `szName`  
  
 `ptkImplementation`  
 fora Um `mdFile` `mdAssemblyRef` token de metadados, ou `mdExportedType` que contém ou permite o acesso às propriedades do tipo exportado.  
  
 `ptkTypeDef`  
 fora Um ponteiro para um `mdTypeDef` token que representa um tipo no arquivo.  
  
 `pdwExportedTypeFlags`  
 fora Um ponteiro para os sinalizadores que descrevem os metadados aplicados ao tipo exportado. O valor de flags pode ser um ou mais valores de [CorTypeAttr](cortypeattr-enumeration.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataAssemblyImport](imetadataassemblyimport-interface.md)
