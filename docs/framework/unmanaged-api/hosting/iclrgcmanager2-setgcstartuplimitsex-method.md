---
description: 'Saiba mais sobre o método: ICLRGCManager2:: SetGCStartupLimitsEx'
title: Método ICLRGCManager2::SetGCStartupLimitsEx
ms.date: 03/30/2017
api_name:
- ICLRGCManager2.SetGCStartupLimitsEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager2::SetCLRGCStartupLimitsEx
helpviewer_keywords:
- ICLRGCManager2::SetGCStartupLimitsEx method [.NET Framework hosting]
- SetGCStartupLimitsEx method, ICLRGCManager2 interface [.NET Framework hosting]
ms.assetid: 6c3a08a9-5d65-48d4-8bbf-2a86ed7d356a
topic_type:
- apiref
ms.openlocfilehash: 2a4801d2f6255f5f84e0a4bae7a1886689ee8dc5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689230"
---
# <a name="iclrgcmanager2setgcstartuplimitsex-method"></a>Método ICLRGCManager2::SetGCStartupLimitsEx

Define o tamanho de um segmento de coleta de lixo e o tamanho máximo da geração 0 do sistema de coleta de lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetGCStartupLimitsEx (  
    [in] SIZE_T SegmentSize,
    [in] SIZE_T MaxGen0Size  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `SegmentSize`  
 no O tamanho especificado de um segmento de coleta de lixo.  
  
 O tamanho mínimo do segmento é 4 MB. Os segmentos podem ser aumentados em incrementos de 1 MB ou mais.  
  
 `MaxGen0Size`  
 no O tamanho máximo especificado para a geração 0.  
  
 O tamanho mínimo de 0 de geração é 64 KB.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`SetGCStartupLimitsEx` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Os valores que `SetGCStartupLimitsEx` conjuntos só podem ser especificados antes do host ser iniciado. As chamadas posteriores para `SetGCStartupLimitsEx` são ignoradas.  
  
 Para definir qualquer parâmetro sem afetar o outro, especifique 0 (zero) para o parâmetro que você não deseja alterar.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Gerenciamento automático de memória](../../../standard/automatic-memory-management.md)
- [Coleta de lixo](../../../standard/garbage-collection/index.md)
- [Interface ICLRControl](iclrcontrol-interface.md)
- [Interface ICLRGCManager2](iclrgcmanager2-interface.md)
