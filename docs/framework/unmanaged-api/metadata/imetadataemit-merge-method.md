---
description: 'Saiba mais sobre o método: IMetaDataEmit:: Merge'
title: Método IMetaDataEmit::Merge
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.Merge
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::Merge
helpviewer_keywords:
- IMetaDataEmit::Merge method [.NET Framework metadata]
- Merge method [.NET Framework metadata]
ms.assetid: 7596220c-f699-4b6c-8ae7-c83220610650
topic_type:
- apiref
ms.openlocfilehash: 6b78dd20555acf1eaf610ed05d8a37ab6cdeee5c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745938"
---
# <a name="imetadataemitmerge-method"></a>Método IMetaDataEmit::Merge

Adiciona o escopo importado especificado à lista de escopos a serem mesclados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Merge (
    [in]  IMetaDataImport  *pImport,
    [in]  IMapToken        *pHostMapToken,
    [in]  IUnknown         *pHandler
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pImport`  
 no Um ponteiro para um objeto [IMetaDataImport](imetadataimport-interface.md) que identifica o escopo importado a ser mesclado.  
  
 `pIMap`  
 no Um ponteiro para um objeto [IMapToken](imaptoken-interface.md) que especifica o novo mapeamento do token.  
  
 `pHandler`  
 no Um ponteiro para um objeto [IUnknown](/cpp/atl/iunknown) que especifica os erros.  
  
## <a name="remarks"></a>Comentários  

 Chame [IMetaDataEmit:: MergeEnd](imetadataemit-mergeend-method.md) para disparar a fusão de metadados em um único escopo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
