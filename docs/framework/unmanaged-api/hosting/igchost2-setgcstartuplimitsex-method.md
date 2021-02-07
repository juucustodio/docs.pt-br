---
description: 'Saiba mais sobre o método: IGCHost2:: SetGCStartupLimitsEx'
title: Método IGCHost2::SetGCStartupLimitsEx
ms.date: 03/30/2017
api_name:
- IGCHost2.SetGCStartupLimitsEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IGCHost2::SetGCStartupLimitsEx
helpviewer_keywords:
- IGCHost2::SetGCStartupLimitsEx method [.NET Framework hosting]
- SetGCStartupLimitsEx method, IGCHost2 interface [.NET Framework hosting]
ms.assetid: bba941c2-1c57-46d3-bbf5-5fb92700c490
topic_type:
- apiref
ms.openlocfilehash: 32d3bcbb467a1a418c7123779c881c46e983edef
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709300"
---
# <a name="igchost2setgcstartuplimitsex-method"></a>Método IGCHost2::SetGCStartupLimitsEx

Define o tamanho do segmento e o tamanho máximo para a geração 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetGCStartupLimitsEx (  
    [in] SIZE_T SegmentSize,  
    [in] SIZE_T MaxGen0Size  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `SegmentSize`  
 no O tamanho do segmento usado pelo sistema de coleta de lixo.  
  
 `MaxGen0Size`  
 no O tamanho máximo para a geração 0.  
  
## <a name="remarks"></a>Comentários  

 Os valores que `SetGCStartupLimitsEx` conjuntos só podem ser especificados antes do host ser iniciado. Esses valores não podem ser alterados posteriormente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** GCHost. idl, GCHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IGCHost2](igchost2-interface.md)
