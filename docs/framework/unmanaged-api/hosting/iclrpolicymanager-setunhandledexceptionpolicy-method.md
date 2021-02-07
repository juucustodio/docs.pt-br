---
description: 'Saiba mais sobre o método: ICLRPolicyManager:: SetUnhandledExceptionPolicy'
title: Método ICLRPolicyManager::SetUnhandledExceptionPolicy
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager.SetUnhandledExceptionPolicy
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager::SetUnhandledExceptionPolicy
helpviewer_keywords:
- ICLRPolicyManager::SetUnhandledExceptionPolicy method [.NET Framework hosting]
- SetUnhandledExceptionPolicy method [.NET Framework hosting]
ms.assetid: 5268480e-280a-4931-b7a3-dc3ffdf7f78f
topic_type:
- apiref
ms.openlocfilehash: 489127bb00b2b65466460baa3cfd31439672cd1c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716530"
---
# <a name="iclrpolicymanagersetunhandledexceptionpolicy-method"></a>Método ICLRPolicyManager::SetUnhandledExceptionPolicy

Especifica o comportamento do Common Language Runtime (CLR) quando ocorre uma exceção sem tratamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetUnhandledExceptionPolicy (  
    [in] EClrUnhandledExceptionPolicy policy  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `policy`  
 no Um dos valores de [EClrUnhandledException](eclrunhandledexception-enumeration.md) , indicando se o comportamento é definido pelo CLR ou pelo host.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`SetUnhandledExceptionPolicy` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Por padrão, o CLR é o manipulador final para todas as exceções sem tratamento e seu comportamento padrão é subdividir o processo. O host pode alterar esse comportamento definindo o `policy` valor como eHostDeterminedPolicy. Esse valor permite que o host implemente seu próprio comportamento padrão, como nas versões anteriores do CLR.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração EClrUnhandledException](eclrunhandledexception-enumeration.md)
- [Interface ICLRControl](iclrcontrol-interface.md)
- [Interface ICLRPolicyManager](iclrpolicymanager-interface.md)
- [Interface IHostPolicyManager](ihostpolicymanager-interface.md)
