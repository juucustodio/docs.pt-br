---
description: 'Saiba mais sobre o método: IMetaDataImport:: FindTypeRef'
title: Método IMetaDataImport::FindTypeRef
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindTypeRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindTypeRef
helpviewer_keywords:
- IMetaDataImport::FindTypeRef method [.NET Framework metadata]
- FindTypeRef method [.NET Framework metadata]
ms.assetid: 1b2bbf3f-943e-412e-b66c-e802431b055c
topic_type:
- apiref
ms.openlocfilehash: 11e966256b5e75c1acff0bf1e6de0c96dc03e6aa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745554"
---
# <a name="imetadataimportfindtyperef-method"></a>Método IMetaDataImport::FindTypeRef

Obtém um ponteiro para o token TypeRef para a <xref:System.Type> referência que está no escopo especificado e que tem o nome especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FindTypeRef (  
   [in] mdToken        tkResolutionScope,  
   [in]  LPCWSTR       szName,  
   [out] mdTypeRef     *ptr  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tkResolutionScope`  
 no Um token ModuleRef, AssemblyRef ou TypeRef que especifica o módulo, o assembly ou o tipo, respectivamente, no qual a referência de tipo é definida.  
  
 `szName`  
 no O nome da referência de tipo a ser pesquisada.  
  
 `ptr`  
 fora Um ponteiro para o token TypeRef correspondente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
