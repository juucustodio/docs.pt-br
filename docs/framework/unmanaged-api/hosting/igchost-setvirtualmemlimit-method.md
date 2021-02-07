---
description: 'Saiba mais sobre o método: IGCHost:: SetVirtualMemLimit'
title: Método IGCHost::SetVirtualMemLimit
ms.date: 03/30/2017
api_name:
- IGCHost.SetVirtualMemLimit
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- SetVirtualMemLimit
helpviewer_keywords:
- IGCHost::SetVirtualMemLimit method [.NET Framework hosting]
- SetVirtualMemLimit method [.NET Framework hosting]
ms.assetid: c7e7c2d0-e58c-4650-b40c-47b2be2cda45
topic_type:
- apiref
ms.openlocfilehash: 62cd9e2d84e51f0544e464bdbf49c50af8086546
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709432"
---
# <a name="igchostsetvirtualmemlimit-method"></a>Método IGCHost::SetVirtualMemLimit

Define o tamanho máximo da memória virtual do tempo de execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetVirtualMemLimit (  
    [in] SIZE_T sztMaxVirtualMemMB  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `sztMaxVirtualMemMB`  
 no O tamanho máximo, em megabytes, da memória virtual do tempo de execução.  
  
## <a name="remarks"></a>Comentários  

 O tamanho máximo da memória virtual do tempo de execução pode ser alterado dinamicamente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** GCHost. idl, GCHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IGCHost](igchost-interface.md)
