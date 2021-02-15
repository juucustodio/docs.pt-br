---
description: 'Saiba mais sobre: método IGCHost:: GetStats'
title: Método IGCHost::GetStats
ms.date: 03/30/2017
api_name:
- IGCHost.GetStats
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- GetStats
helpviewer_keywords:
- GetStats method, IGCHost interface [.NET Framework hosting]
- IGCHost::GetStats method [.NET Framework hosting]
ms.assetid: c4ae022c-46ac-4f19-9ddd-09b955f19412
topic_type:
- apiref
ms.openlocfilehash: 564224d01e23c8ac1fe81025ee87dabc41ed5166
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709672"
---
# <a name="igchostgetstats-method"></a>Método IGCHost::GetStats

Obtém as estatísticas do estado atual do sistema de coleta de lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetStats (  
    [in, out] COR_GC_STATS *pStats  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pStats`  
 [entrada, saída] Um ponteiro para uma estrutura de [COR_GC_STATS](cor-gc-stats-structure.md) que contém as estatísticas para o estado atual do sistema de coleta de lixo.  
  
## <a name="remarks"></a>Comentários  

 As estatísticas podem ser usadas por um sistema de alocação inteligente para ajudar o sistema de coleta de lixo a funcionar. Por exemplo, o sistema de alocação pode determinar, depois de revisar as estatísticas, que precisa adicionar mais memória ou forçar uma coleta.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** GCHost. idl, GCHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IGCHost](igchost-interface.md)
