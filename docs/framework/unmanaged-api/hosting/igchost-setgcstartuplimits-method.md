---
description: 'Saiba mais sobre o método: IGCHost:: SetGCStartupLimits'
title: Método IGCHost::SetGCStartupLimits
ms.date: 03/30/2017
api_name:
- IGCHost.SetGCStartupLimits
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- SetGCStartupLimits
helpviewer_keywords:
- SetGCStartupLimits method, IGCHost interface [.NET Framework hosting]
- IGCHost::SetGCStartupLimits method [.NET Framework hosting]
ms.assetid: cae53926-82ac-4d1d-b297-0bde0bd1bebb
topic_type:
- apiref
ms.openlocfilehash: 91c74d54189bbfb7e9f208e507fe6e75b7023e00
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709471"
---
# <a name="igchostsetgcstartuplimits-method"></a>Método IGCHost::SetGCStartupLimits

Define o tamanho do segmento e o tamanho máximo para a geração 0.  
  
> [!IMPORTANT]
> A partir do .NET Framework 4,5, você pode definir o tamanho do segmento e o tamanho máximo de geração 0 para valores maiores do que `DWORD` usar o método [IGCHost2:: SetGCStartupLimitsEx](igchost2-setgcstartuplimitsex-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetGCStartupLimits (  
    [in] DWORD SegmentSize,  
    [in] DWORD MaxGen0Size  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `SegmentSize`  
 no O tamanho do segmento usado pelo sistema de coleta de lixo.  
  
 `MaxGen0Size`  
 no O tamanho máximo para a geração 0.  
  
## <a name="remarks"></a>Comentários  

 O `SetGCStartupLimits` método pode ser chamado apenas uma vez. Esses valores não podem ser alterados posteriormente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** GCHost. idl, GCHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IGCHost](igchost-interface.md)
