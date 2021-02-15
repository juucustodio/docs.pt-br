---
description: 'Saiba mais sobre: IMetaDataEmit: método efineMemberRef de:D'
title: Método IMetaDataEmit::DefineMemberRef
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineMemberRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineMemberRef
helpviewer_keywords:
- DefineMemberRef method [.NET Framework metadata]
- IMetaDataEmit::DefineMemberRef method [.NET Framework metadata]
ms.assetid: 21b5bcb8-ea75-4962-8acc-ad17584061e5
topic_type:
- apiref
ms.openlocfilehash: 1d88294cea14369c8a8f16b6048f96472fbb9502
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753413"
---
# <a name="imetadataemitdefinememberref-method"></a>Método IMetaDataEmit::DefineMemberRef

Define uma referência a um membro de um módulo fora do escopo atual e Obtém um token para essa definição de referência.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineMemberRef (
    [in]  mdToken           tkImport,
    [in]  LPCWSTR           szName,
    [in]  PCCOR_SIGNATURE   pvSigBlob,
    [in]  ULONG             cbSigBlob,
    [out] mdMemberRef       *pmr
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tkImport`  
 no Token para a classe ou a interface do membro de destino, se o membro não for global; Se o membro for global, o `mdModuleRef` token para esse outro arquivo.  
  
 `szName`  
 no O nome do membro de destino.  
  
 `pvSigBlob`  
 no A assinatura do membro de destino.  
  
 `cbSigBlob`  
 no A contagem de bytes em `pvSigBlob` .  
  
 `pmr`  
 fora O `mdMemberRef` token atribuído.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
