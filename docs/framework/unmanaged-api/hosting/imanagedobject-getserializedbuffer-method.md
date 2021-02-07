---
description: 'Saiba mais sobre o método: IManagedObject:: GetSerializedBuffer'
title: Método IManagedObject::GetSerializedBuffer
ms.date: 03/30/2017
api_name:
- IManagedObject.GetSerializedBuffer
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- GetSerializedBuffer
helpviewer_keywords:
- IManagedObject::GetSerializedBuffer method [.NET Framework hosting]
- GetSerializedBuffer method [.NET Framework hosting]
ms.assetid: c17105bb-b49f-434e-8f9b-77f8c85b9220
topic_type:
- apiref
ms.openlocfilehash: f324b6ed1e9cea21fec9027a954fbad54174dd0c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753764"
---
# <a name="imanagedobjectgetserializedbuffer-method"></a>Método IManagedObject::GetSerializedBuffer

Obtém a representação da cadeia de caracteres deste objeto gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSerializedBuffer (  
    [out] BSTR *pBSTR  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pBSTR`  
 fora Um ponteiro para uma cadeia de caracteres que é o objeto serializado.  
  
## <a name="remarks"></a>Comentários  

 O `GetSerializedBuffer` método serializa o objeto para que ele possa ser empacotado para o cliente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IManagedObject](imanagedobject-interface.md)
