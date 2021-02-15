---
description: 'Saiba mais sobre o método: ICeeGen:: TruncateSection'
title: Método ICeeGen::TruncateSection
ms.date: 03/30/2017
api_name:
- ICeeGen.TruncateSection
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen::TruncateSection
helpviewer_keywords:
- TruncateSection method [.NET Framework metadata]
- ICeeGen::TruncateSection method [.NET Framework metadata]
ms.assetid: 0451d752-1e5c-4c9a-8bad-6cd35b7ba3df
topic_type:
- apiref
ms.openlocfilehash: 074c7d7b4222b5b22f1d9b79169d531cd5544b1e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784204"
---
# <a name="iceegentruncatesection-method"></a>Método ICeeGen::TruncateSection

Trunca a seção de código especificada pelo comprimento especificado.  
  
 Este método é obsoleto e não deve ser usado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT TruncateSection (  
    [in]  HCEESECTION     section,  
    [in]  ULONG           len  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `section`  
 no A seção a ser truncada.  
  
 `len`  
 no O comprimento, em bytes, pelo qual truncar a seção.  
  
## <a name="remarks"></a>Comentários  

 Chame `TruncateSection` somente se você tiver requisitos de seção especiais que não são tratados por outros métodos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICeeGen](iceegen-interface.md)
