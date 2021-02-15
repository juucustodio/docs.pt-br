---
description: 'Saiba mais sobre o método: IHostControl:: GetHostManager'
title: Método IHostControl::GetHostManager
ms.date: 03/30/2017
api_name:
- IHostControl.GetHostManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostControl::GetHostManager
helpviewer_keywords:
- GetHostManager method [.NET Framework hosting]
- IHostControl::GetHostManager method [.NET Framework hosting]
ms.assetid: 0fa34bca-ed18-4626-9e78-d33684d18edb
topic_type:
- apiref
ms.openlocfilehash: 7cc118808c8788504da2cc07a8c61c419d3c588f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99708889"
---
# <a name="ihostcontrolgethostmanager-method"></a>Método IHostControl::GetHostManager

Obtém um ponteiro de interface para a implementação do host da interface com o especificado `IID` .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetHostManager (  
    [in] REFIID riid,  
    [out, iid_is(riid)] void** ppObject  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `riid`  
 no O `IID` da interface que o Common Language Runtime (CLR) está consultando.  
  
 `ppObject`  
 fora Um ponteiro para a interface implementada pelo host, ou NULL se o host não oferecer suporte a essa interface.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`GetHostManager` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_INVALIDARG|O solicitado `IID` não é válido.|  
|E_NOINTERFACE|Não há suporte para a interface solicitada.|  
  
## <a name="remarks"></a>Comentários  

 O CLR consulta o host para determinar se ele dá suporte a uma ou mais das seguintes interfaces:  
  
- [IHostMemoryManager](ihostmemorymanager-interface.md)  
  
- [IHostTaskManager](ihosttaskmanager-interface.md)  
  
- [IHostThreadPoolManager](ihostthreadpoolmanager-interface.md)  
  
- [IHostIoCompletionManager](ihostiocompletionmanager-interface.md)  
  
- [IHostSyncManager](ihostsyncmanager-interface.md)  
  
- [IHostAssemblyManager](ihostassemblymanager-interface.md)  
  
- [IHostGCManager](ihostgcmanager-interface.md)  
  
- [O IHostPolicyManager](ihostpolicymanager-interface.md)  
  
- [IHostSecurityManager](ihostsecuritymanager-interface.md)  
  
 Se o host oferecer suporte à interface especificada, ele definirá `ppObject` como sua implementação dessa interface. Caso contrário, ele será definido `ppObject` como NULL.  
  
 O CLR não chama `Release` os gerenciadores de host, mesmo quando você o desliga.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostControl](ihostcontrol-interface.md)
