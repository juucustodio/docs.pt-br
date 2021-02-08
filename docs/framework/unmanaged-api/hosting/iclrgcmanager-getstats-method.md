---
description: 'Saiba mais sobre: método ICLRGCManager:: GetStats'
title: Método ICLRGCManager::GetStats
ms.date: 03/30/2017
api_name:
- ICLRGCManager.GetStats
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager::GetStats
helpviewer_keywords:
- GetStats method, ICLRGCManager interface [.NET Framework hosting]
- ICLRGCManager::GetStats method [.NET Framework hosting]
ms.assetid: ce259d1d-cd81-4490-a7a1-0d0ea0804872
topic_type:
- apiref
ms.openlocfilehash: 94b20fb313f06d73f1e7fafd1f46fefb0da3fe95
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790016"
---
# <a name="iclrgcmanagergetstats-method"></a>Método ICLRGCManager::GetStats

Obtém um conjunto de estatísticas atuais sobre o sistema de coleta de lixo do Common Language Runtime.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetStats (  
    [in, out] COR_GC_STATS *pStats  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pStats`  
 [entrada, saída] Uma instância de [COR_GC_STATS](cor-gc-stats-structure.md) que contém as estatísticas solicitadas.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`GetStats` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O CLR calcula e retorna somente as estatísticas que são especificadas pelo `Flags` campo de `pStats` .  
  
 Defina o `Flags` campo como um ou mais valores da enumeração [COR_GC_STAT_TYPES](cor-gc-stat-types-enumeration.md) para especificar quais estatísticas na estrutura de [COR_GC_STATS](cor-gc-stats-structure.md) devem ser definidas.  
  
 Um exemplo de uso é o seguinte:  
  
```cpp  
COR_GC_STATS GCStats;  
GCStats.Flags = COR_GC_COUNTS | COR_GC_MEMORYUSAGE;  
pCLRGCManager->GetStats(&GCStats);  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Gerenciamento automático de memória](../../../standard/automatic-memory-management.md)
- [Estrutura COR_GC_STATS](cor-gc-stats-structure.md)
- [Enumeração COR_GC_STAT_TYPES](cor-gc-stat-types-enumeration.md)
- [Coleta de lixo](../../../standard/garbage-collection/index.md)
- [Interface ICLRControl](iclrcontrol-interface.md)
- [Interface ICLRGCManager](iclrgcmanager-interface.md)
- [Interfaces de hospedagem CLR](clr-hosting-interfaces.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
