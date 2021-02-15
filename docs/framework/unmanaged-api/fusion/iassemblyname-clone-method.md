---
description: 'Saiba mais sobre o método: IAssemblyName:: clone'
title: Método IAssemblyName::Clone
ms.date: 03/30/2017
api_name:
- IAssemblyName.Clone
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyName::Clone
helpviewer_keywords:
- Clone method, IAssemblyName interface [.NET Framework fusion]
- IAssemblyName::Clone method [.NET Framework fusion]
ms.assetid: 7b345e08-5e16-4e3d-a044-4e19d0892943
topic_type:
- apiref
ms.openlocfilehash: b1d8ba2aec73565e9f6acaa44a5ef3731baa3af9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760778"
---
# <a name="iassemblynameclone-method"></a>Método IAssemblyName::Clone

Cria uma cópia superficial deste objeto [IAssemblyName](iassemblyname-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Clone (  
    [out] IAssemblyName **pName  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pName`  
 fora A cópia retornada deste `IAssemblyName` objeto.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IAssemblyName](iassemblyname-interface.md)
