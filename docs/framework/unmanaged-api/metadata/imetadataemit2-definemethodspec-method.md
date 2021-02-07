---
description: 'Saiba mais sobre: IMetaDataEmit2: método efineMethodSpec de:D'
title: Método IMetaDataEmit2::DefineMethodSpec
ms.date: 03/30/2017
api_name:
- IMetaDataEmit2.DefineMethodSpec
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit2::DefineMethodSpec
helpviewer_keywords:
- DefineMethodSpec method [.NET Framework metadata]
- IMetaDataEmit2::DefineMethodSpec method [.NET Framework metadata]
ms.assetid: 3c24e552-fc69-4971-b65a-a3e4b5f7f1e8
topic_type:
- apiref
ms.openlocfilehash: 4b5283375ba194a86a83b142b3b2bdc06bfd35da
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745730"
---
# <a name="imetadataemit2definemethodspec-method"></a>Método IMetaDataEmit2::DefineMethodSpec

Cria uma instância genérica de um método e Obtém um token para a definição.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineMethodSpec (  
    [in]  mdToken           tkParent,
    [in]  PCCOR_SIGNATURE   pvSigBlob,
    [in]  ULONG             cbSigBlob,
    [out] mdMethodSpec      *pmi  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tkParent`  
 no Um token para o método do qual criar a instância genérica. O token deve ser do tipo `mdMethodDef` ou `mdMemberRef` .  
  
 `pvSigBlob`  
 no Um ponteiro para a assinatura COM+ binária do método.  
  
 `cbSibBlob`  
 no O tamanho, em bytes, de `pvSigBlob` .  
  
 `pmi`  
 fora Um token para a definição de assinatura de metadados do método.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
- [Interface IMetaDataEmit](imetadataemit-interface.md)
