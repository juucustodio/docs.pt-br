---
description: 'Saiba mais sobre o método: IMetaDataEmit:: GetTokenFromTypeSpec'
title: Método IMetaDataEmit::GetTokenFromTypeSpec
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.GetTokenFromTypeSpec
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::GetTokenFromTypeSpec
helpviewer_keywords:
- GetTokenFromTypeSpec method [.NET Framework metadata]
- IMetaDataEmit::GetTokenFromTypeSpec method [.NET Framework metadata]
ms.assetid: 7de6447a-a751-49d8-87e2-951cee77b536
topic_type:
- apiref
ms.openlocfilehash: 09f7133af9b9d912b03cdc1c93744ee260c69169
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728230"
---
# <a name="imetadataemitgettokenfromtypespec-method"></a>Método IMetaDataEmit::GetTokenFromTypeSpec

Obtém um token de metadados para o tipo com a assinatura de metadados especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetTokenFromTypeSpec (
    [in]  PCCOR_SIGNATURE       pvSig,
    [in]  ULONG                 cbSig,
    [out] mdTypeSpec            *ptypespec
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pvSig`  
 no A assinatura que está sendo definida.  
  
 `cbSig`  
 no A contagem de bytes em `pvSig` .  
  
 `ptypespec`  
 fora O `mdTypeSpec` token atribuído.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
