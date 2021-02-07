---
description: 'Saiba mais sobre o método: IMapToken:: map'
title: Método IMapToken::Map
ms.date: 03/30/2017
api_name:
- IMapToken.Map
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMapToken::Map
helpviewer_keywords:
- IMapToken::Map method [.NET Framework metadata]
- Map method [.NET Framework metadata]
ms.assetid: b9b4bf2f-1098-43d6-9619-a99b4bda1940
topic_type:
- apiref
ms.openlocfilehash: da78f22e944a0e4ec25adcd7cdf97b69131a6612
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99706728"
---
# <a name="imaptokenmap-method"></a>Método IMapToken::Map

Mapeia uma relação entre os assemblies usando assinaturas de metadados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Map (  
    [in]  mdToken tkImp,
    [in]  mdToken tkEmit  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tkImp`  
 no O token de metadados que representa o objeto de código importado.  
  
 `tkEmit`  
 no O token de metadados que representa o objeto de código emitido.  
  
## <a name="remarks"></a>Comentários  

 Quando o novo mapeamento de token ocorre durante uma mesclagem, o token original é definido no escopo de metadados importado (origem) e o novo token é definido no escopo de metadados emitido (destino).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMapToken](imaptoken-interface.md)
