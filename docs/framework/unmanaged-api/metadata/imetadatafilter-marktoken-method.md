---
description: 'Saiba mais sobre o método: IMetaDataFilter:: MarkToken'
title: Método IMetaDataFilter::MarkToken
ms.date: 03/30/2017
api_name:
- IMetaDataFilter.MarkToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataFilter::MarkToken
helpviewer_keywords:
- IMetaDataFilter::MarkToken method [.NET Framework metadata]
- MarkToken method, IMetaDataFilter interface [.NET Framework metadata]
ms.assetid: bd492834-6529-4d39-b93d-f8cdbd3e297f
topic_type:
- apiref
ms.openlocfilehash: 97191533ae7d2bdc951521f1929a4c001c521b9d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99677768"
---
# <a name="imetadatafiltermarktoken-method"></a>Método IMetaDataFilter::MarkToken

Define um valor que indica que o token de metadados especificado foi processado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT MarkToken (  
    [in] mdToken   tk  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tk`  
 no O token a ser marcado como processado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataFilter](imetadatafilter-interface.md)
