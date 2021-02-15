---
description: 'Saiba mais sobre o método: IMetaDataEmit:: GetTokenFromSig'
title: Método IMetaDataEmit::GetTokenFromSig
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.GetTokenFromSig
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::GetTokenFromSig
helpviewer_keywords:
- IMetaDataEmit::GetTokenFromSig method [.NET Framework metadata]
- GetTokenFromSig method [.NET Framework metadata]
ms.assetid: 50a58a83-6287-40a4-b315-47823cea0a5c
topic_type:
- apiref
ms.openlocfilehash: 3b9b38389a2bf78a65baa2cf96e3a422c54d0bcb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783918"
---
# <a name="imetadataemitgettokenfromsig-method"></a>Método IMetaDataEmit::GetTokenFromSig

Obtém um token para a assinatura de metadados especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetTokenFromSig (
    [in]  PCCOR_SIGNATURE pvSig,
    [in]  ULONG       cbSig,
    [out] mdSignature *pmsig
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pvSig`  
 no A assinatura a ser persistida e armazenada.  
  
 `cbSig`  
 no A contagem de bytes em `pvSig` .  
  
 `pmsig`  
 fora O `mdSignature` token atribuído.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
