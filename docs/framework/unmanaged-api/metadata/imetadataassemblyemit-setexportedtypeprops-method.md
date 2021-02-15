---
description: 'Saiba mais sobre o método: IMetaDataAssemblyEmit:: SetExportedTypeProps'
title: Método IMetaDataAssemblyEmit::SetExportedTypeProps
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.SetExportedTypeProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::SetExportedTypeProps
helpviewer_keywords:
- SetExportedTypeProps method [.NET Framework metadata]
- IMetaDataAssemblyEmit::SetExportedTypeProps method [.NET Framework metadata]
ms.assetid: 1c090153-fd5f-46c7-9cff-39a78d992c8f
topic_type:
- apiref
ms.openlocfilehash: 61032abd7b049af29c583e9aee126184af3c78f2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99678088"
---
# <a name="imetadataassemblyemitsetexportedtypeprops-method"></a>Método IMetaDataAssemblyEmit::SetExportedTypeProps

Modifica a estrutura de `ExportedType` metadados especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetExportedTypeProps (  
    [in] mdExportedType   ct,
    [in] mdToken          tkImplementation,  
    [in] mdTypeDef        tkTypeDef,  
    [in] DWORD            dwExportedTypeFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ct`  
 no O token de metadados que especifica a `ExportedType` estrutura de metadados a ser modificada.  
  
 `tkImplementation`  
 no O token, do tipo `File` , `AssemblyRef` ou `ExportedType` , que especifica como esse tipo é implementado.  
  
 `tkTypeDef`  
 no O `TypeDef` token referenciado no arquivo de código.  
  
 `dwExportedTypeFlags`  
 no Uma combinação de bits de valores que especifica atributos do tipo.  
  
## <a name="remarks"></a>Comentários  

 Para criar uma `ExportedType` estrutura de metadados, use o método [IMetaDataAssemblyEmit::D efineexportedtype](imetadataassemblyemit-defineexportedtype-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataAssemblyEmit](imetadataassemblyemit-interface.md)
