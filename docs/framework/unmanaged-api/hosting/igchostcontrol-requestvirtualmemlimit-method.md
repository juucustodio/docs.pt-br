---
description: 'Saiba mais sobre o método: IGCHostControl:: RequestVirtualMemLimit'
title: Método IGCHostControl::RequestVirtualMemLimit
ms.date: 03/30/2017
api_name:
- IGCHostControl.RequestVirtualMemLimit
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- RequestVirtualMemLimit
helpviewer_keywords:
- IGCHostControl::RequestVirtualMemLimit method [.NET Framework hosting]
- RequestVirtualMemLimit method [.NET Framework hosting]
ms.assetid: f4984a8c-4c0e-4460-9aa1-d022b3621228
topic_type:
- apiref
ms.openlocfilehash: b0ee22671b63be0ed0d23ebb103a6a5a7ca9f2b9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709380"
---
# <a name="igchostcontrolrequestvirtualmemlimit-method"></a>Método IGCHostControl::RequestVirtualMemLimit

Solicita que o host altere os limites de memória virtual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT RequestVirtualMemLimit (  
    [in] SIZE_T       sztMaxVirtualMemMB,  
    [in, out] SIZE_T* psztNewMaxVirtualMemMB  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `sztMaxVirtualMemMB`  
 no O tamanho solicitado da memória a ser alocada.  
  
 `psztNewMaxVirtualMemMB`  
 [entrada, saída] Um ponteiro para o tamanho real da memória alocada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IGCHostControl](igchostcontrol-interface.md)
