---
description: 'Saiba mais sobre o método: ICLRPolicyManager:: SetActionOnTimeout'
title: Método ICLRPolicyManager::SetActionOnTimeout
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager.SetActionOnTimeout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager::SetActionOnTimeout
helpviewer_keywords:
- SetActionOnTimeout method [.NET Framework hosting]
- ICLRPolicyManager::SetActionOnTimeout method [.NET Framework hosting]
ms.assetid: 38439fa1-2b99-4fa8-a6ec-08afc0f83b9c
topic_type:
- apiref
ms.openlocfilehash: d682acd49bdc4fa0f8c58a1300e2215816fe2718
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689021"
---
# <a name="iclrpolicymanagersetactionontimeout-method"></a>Método ICLRPolicyManager::SetActionOnTimeout

Especifica a ação de política que o Common Language Runtime (CLR) deve executar quando a operação especificada atingir o tempo limite.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetActionOnTimeout (  
    [in] EClrOperation operation,  
    [in] EPolicyAction action  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `operation`  
 no Um dos valores de [EClrOperation](eclroperation-enumeration.md) , que indica a operação para a qual especificar a ação de tempo limite. Os seguintes valores têm suporte:  
  
- OPR_AppDomainUnload  
  
- OPR_ProcessExit  
  
- OPR_ThreadRudeAbortInCriticalRegion  
  
- OPR_ThreadRudeAbortInNonCriticalRegion  
  
 `action`  
 no Um dos valores de [EPolicyAction](epolicyaction-enumeration.md) , indicando a ação da política a ser executada quando a operação atingir o tempo limite.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`SetActionOnTimeout` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_INVALIDARG|Não é possível definir um tempo limite para o especificado `operation` ou um valor inválido foi fornecido para `operation` .|  
  
## <a name="remarks"></a>Comentários  

 O valor de tempo limite pode ser o tempo limite padrão definido pelo CLR ou um valor especificado pelo host em uma chamada para o método [ICLRPolicyManager:: SetTimeout](iclrpolicymanager-settimeout-method.md) .  
  
 Nem todos os valores de ação de política podem ser especificados como o comportamento de tempo limite para operações de CLR. `SetActionOnTimeout` normalmente é usado apenas para escalonar o comportamento. Por exemplo, um host pode especificar que as anulações de thread sejam transformadas em anulações de thread rudes, mas não podem especificar o oposto. A tabela a seguir descreve os `action` valores válidos para os `operation` valores válidos.  
  
|Valor de `operation`|Valores válidos para `action`|  
|---------------------------|-------------------------------|  
|OPR_ThreadRudeAbortInNonCriticalRegion<br /><br /> OPR_ThreadRudeAbortInCriticalRegion|- eRudeAbortThread<br />- eUnloadAppDomain<br />- eRudeUnloadAppDomain<br />- eExitProcess<br />- eFastExitProcess<br />- eRudeExitProcess<br />- eDisableRuntime|  
|OPR_AppDomainUnload|- eUnloadAppDomain<br />- eRudeUnloadAppDomain<br />- eExitProcess<br />- eFastExitProcess<br />- eRudeExitProcess<br />- eDisableRuntime|  
|OPR_ProcessExit|- eExitProcess<br />- eFastExitProcess<br />- eRudeExitProcess<br />- eDisableRuntime|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração EClrOperation](eclroperation-enumeration.md)
- [Enumeração EPolicyAction](epolicyaction-enumeration.md)
- [Interface ICLRControl](iclrcontrol-interface.md)
- [Interface ICLRPolicyManager](iclrpolicymanager-interface.md)
