---
description: 'Saiba mais sobre o método: IHostFilter:: MarkToken'
title: Método IHostFilter::MarkToken
ms.date: 03/30/2017
api_name:
- IHostFilter.MarkToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostFilter::MarkToken
helpviewer_keywords:
- MarkToken method, IHostFilter interface [.NET Framework metadata]
- IHostFilter::MarkToken method [.NET Framework metadata]
ms.assetid: d7061343-d0a3-4fd5-b312-61974f98bd62
topic_type:
- apiref
ms.openlocfilehash: c8f5ecdef56b77e1b0031a93d6d8f7de79de4c3b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784178"
---
# <a name="ihostfiltermarktoken-method"></a>Método IHostFilter::MarkToken

Indica que o token de metadados especificado será processado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT MarkToken (  
    [in]  mdToken         tk  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tk`  
 no O token de metadados a ser processado.  
  
## <a name="remarks"></a>Comentários  

 Normalmente, você deseja que um token seja processado se ele estiver no escopo de metadados. O `MarkToken` método é passado para o mecanismo de metadados por meio do método [IMetaDataEmit:: sethandlers](imetadataemit-sethandler-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de metadados](metadata-interfaces.md)
- [Interface IHostFilter](ihostfilter-interface.md)
