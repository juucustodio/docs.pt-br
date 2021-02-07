---
description: 'Saiba mais sobre o método: IMetaDataError:: OnError'
title: Método IMetaDataError::OnError
ms.date: 03/30/2017
api_name:
- IMetaDataError.OnError
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataError::OnError
helpviewer_keywords:
- IMetaDataError::OnError method [.NET Framework metadata]
- OnError method, IMetaDataError interface [.NET Framework metadata]
ms.assetid: c1e744b8-a6fb-4d9c-a971-8babc875d8f0
topic_type:
- apiref
ms.openlocfilehash: 9556f1bd7758755d9160e3a2e91a1fe5786aa562
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99670964"
---
# <a name="imetadataerroronerror-method"></a>Método IMetaDataError::OnError

Fornece uma notificação de erros que ocorrem durante a mesclagem de metadados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT OnError (  
    [in] HRESULT   hrError,
    [in] mdToken   token  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `hrError`  
 no O valor de erro HRESULT retornado ao método de chamada.  
  
 `token`  
 no O token de metadados do objeto de código que estava sendo mesclado quando o erro ocorreu.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataError](imetadataerror-interface.md)
