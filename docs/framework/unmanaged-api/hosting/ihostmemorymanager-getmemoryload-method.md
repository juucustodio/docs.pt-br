---
description: 'Saiba mais sobre o método: IHostMemoryManager:: GetMemoryLoad'
title: Método IHostMemoryManager::GetMemoryLoad
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.GetMemoryLoad
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::GetMemoryLoad
helpviewer_keywords:
- IHostMemoryManager::GetMemoryLoad method [.NET Framework hosting]
- GetMemoryLoad method [.NET Framework hosting]
ms.assetid: e8138f6e-a0a4-48d4-8dae-9466b4dc6180
topic_type:
- apiref
ms.openlocfilehash: 82288e6a705b014c2768c75e15376f7e6a0af428
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99707835"
---
# <a name="ihostmemorymanagergetmemoryload-method"></a>Método IHostMemoryManager::GetMemoryLoad

Obtém a quantidade de memória física que está em uso no momento e, portanto, indisponível, conforme relatado pelo host.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMemoryLoad (  
    [out] DWORD*  pMemoryLoad,
    [out] SIZE_T  *pAvailableBytes  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pMemoryLoad`  
 fora Um ponteiro para a porcentagem aproximada da memória física total que está em uso no momento.  
  
 `pAvailableBytes`  
 fora Um ponteiro para o número de bytes disponíveis para o Common Language Runtime (CLR).  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`GetMemoryLoad` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 `GetMemoryLoad` encapsula a função do Win32 `GlobalMemoryStatus` . O valor de `pMemoryLoad` é o equivalente do `dwMemoryLoad` campo na `MEMORYSTATUS` estrutura retornada de `GlobalMemoryStatus` .  
  
 O tempo de execução usa o valor de retorno como uma heurística para o coletor de lixo. Por exemplo, se o host relatar que a maior parte da memória está em uso, o coletor de lixo poderá optar por coletar de várias gerações para aumentar a quantidade de memória que pode ser disponibilizada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.GC?displayProperty=nameWithType>
- [Interface IHostMemoryManager](ihostmemorymanager-interface.md)
