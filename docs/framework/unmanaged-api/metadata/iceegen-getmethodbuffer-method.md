---
description: 'Saiba mais sobre o método: ICeeGen:: GetMethodBuffer'
title: Método ICeeGen::GetMethodBuffer
ms.date: 03/30/2017
api_name:
- ICeeGen.GetMethodBuffer
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen::GetMethodBuffer
helpviewer_keywords:
- ICeeGen::GetMethodBuffer method [.NET Framework metadata]
- GetMethodBuffer method [.NET Framework metadata]
ms.assetid: c7c5b39a-d4ac-41f1-9d1e-44163f563a49
topic_type:
- apiref
ms.openlocfilehash: 24811f231b1db6d985753d4f4695f432aa12edc2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99706923"
---
# <a name="iceegengetmethodbuffer-method"></a>Método ICeeGen::GetMethodBuffer

Obtém um buffer do tamanho apropriado para o método no endereço virtual relativo especificado.  
  
 Este método é obsoleto e não deve ser usado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMethodBuffer (  
    [in]  ULONG       RVA,  
    [out] UCHAR       **lpBuffer  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `RVA`  
 no O endereço virtual relativo do método para o qual retornar um buffer.  
  
 `lpBuffer`  
 fora Um ponteiro para o buffer retornado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICeeGen](iceegen-interface.md)
