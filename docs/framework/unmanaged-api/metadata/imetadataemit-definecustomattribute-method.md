---
description: 'Saiba mais sobre: IMetaDataEmit: método efineCustomAttribute de:D'
title: Método IMetaDataEmit::DefineCustomAttribute
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineCustomAttribute
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineCustomAttribute
helpviewer_keywords:
- DefineCustomAttribute method [.NET Framework metadata]
- IMetaDataEmit::DefineCustomAttribute method [.NET Framework metadata]
ms.assetid: 7dd14854-b756-4401-b167-88ca576dc8f0
topic_type:
- apiref
ms.openlocfilehash: 5d802f590525b8b398ac270b1b7f59d122b45b73
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753478"
---
# <a name="imetadataemitdefinecustomattribute-method"></a>Método IMetaDataEmit::DefineCustomAttribute

Cria uma definição para um atributo personalizado com a assinatura de metadados especificada, a ser anexada ao objeto especificado e Obtém um token para essa definição de atributo personalizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineCustomAttribute (
    [in]  mdToken     tkObj,
    [in]  mdToken     tkType,
    [in]  void const  *pCustomAttribute,
    [in]  ULONG       cbCustomAttribute,
    [out] mdCustomAttribute *pcv
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tkObj`  
 no O token para o item de proprietário.  
  
 `tkType`  
 no O token que identifica o atributo personalizado.  
  
 `pCustomAttribute`  
 no Um ponteiro para o atributo personalizado.  
  
 `cbCustomAttribute`  
 no A contagem de bytes em `pCustomAttribute` .  
  
 `pcv`  
 fora O `mdCustomAttribute` token atribuído.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
