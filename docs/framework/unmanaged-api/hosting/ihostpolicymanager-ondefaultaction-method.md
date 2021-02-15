---
description: 'Saiba mais sobre o método: O IHostPolicyManager:: OnDefaultAction'
title: Método IHostPolicyManager::OnDefaultAction
ms.date: 03/30/2017
api_name:
- IHostPolicyManager.OnDefaultAction
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostPolicyManager::OnDefaultAction
helpviewer_keywords:
- OnDefaultAction method [.NET Framework hosting]
- IHostPolicyManager::OnDefaultAction method [.NET Framework hosting]
ms.assetid: 071e73bd-4795-470f-9373-cfaef553b7f2
topic_type:
- apiref
ms.openlocfilehash: ea474734f7bc0a5210c5aecf605452909b261a87
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99671900"
---
# <a name="ihostpolicymanagerondefaultaction-method"></a>Método IHostPolicyManager::OnDefaultAction

Notifica o host que o Common Language Runtime (CLR) está prestes a executar a ação padrão que foi definida por uma chamada para o método [ICLRPolicyManager:: Setpadrãoaction](iclrpolicymanager-setdefaultaction-method.md) em resposta a uma anulação ou <xref:System.AppDomain> descarregamento de thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT OnDefaultAction (  
    [in] EClrOperation  operation,
    [in] EPolicyAction  action  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `operation`  
 no Um dos valores de [EClrOperation](eclroperation-enumeration.md) , indicando o tipo de evento para o qual o CLR está respondendo.  
  
 `action`  
 no Um dos valores de [EPolicyAction](epolicyaction-enumeration.md) , indicando a ação que o CLR está realizando em resposta ao evento.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`OnDefaultAction` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada. com êxito|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração EClrOperation](eclroperation-enumeration.md)
- [Enumeração EPolicyAction](epolicyaction-enumeration.md)
- [Interface ICLRPolicyManager](iclrpolicymanager-interface.md)
- [Interface IHostPolicyManager](ihostpolicymanager-interface.md)
