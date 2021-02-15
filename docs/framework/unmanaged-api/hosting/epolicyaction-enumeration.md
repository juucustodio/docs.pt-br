---
description: 'Saiba mais sobre: Enumeração EPolicyAction'
title: Enumeração EPolicyAction
ms.date: 03/30/2017
api_name:
- EPolicyAction
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EPolicyAction
helpviewer_keywords:
- EPolicyAction enumeration [.NET Framework hosting]
ms.assetid: 72dd76ba-239e-45ac-9ded-318fb07d6c6d
topic_type:
- apiref
ms.openlocfilehash: fb66de2211972bd4d25ccfbab4965f315c0144a2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785445"
---
# <a name="epolicyaction-enumeration"></a>Enumeração EPolicyAction

Descreve as ações de política que o host pode definir para operações descritas por [EClrOperation](eclroperation-enumeration.md) e falhas descritas por [EClrFailure](eclrfailure-enumeration.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    eNoAction,  
    eThrowException,  
    eAbortThread,  
    eRudeAbortThread,  
    eUnloadAppDomain,  
    eRudeUnloadAppDomain,  
    eExitProcess,  
    eFastExitProcess,  
    eRudeExitProcess,  
    eDisableRuntime  
} EPolicyAction;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`eAbortThread`|Especifica que o Common Language Runtime (CLR) deve abortar o thread normalmente. Uma anulação normal inclui tentativas de executar todos os `finally` blocos, todos os `catch` blocos relacionados a anulações de thread e finalizadores.|  
|`eDisableRuntime`|Especifica que o CLR deve entrar em um estado desabilitado. Nenhum código gerenciado adicional pode ser executado no processo afetado e os threads são impedidos de entrar no CLR.|  
|`eExitProcess`|Especifica que o CLR deve tentar uma saída normal do processo, incluindo a execução de finalizadores e a execução de operações de limpeza e registro em log.|  
|`eFastExitProcess`|Especifica que o CLR deve sair do processo imediatamente, sem executar finalizadores ou executar operações de limpeza e registro em log. No entanto, a notificação é enviada ao depurador.|  
|`eNoAction`|Especifica que nenhuma ação deve ser executada.|  
|`eRudeAbortThread`|Especifica que o CLR deve executar uma anulação de thread rude. Somente os `catch` `finally` blocos and marcados com <xref:System.EnterpriseServices.MustRunInClientContextAttribute> são executados.|  
|`eRudeExitProcess`|Especifica que o CLR deve sair do processo sem executar finalizadores ou operações de registro em log.|  
|`eRudeUnloadAppDomain`|Especifica que o CLR deve executar um descarregamento rude do <xref:System.AppDomain> . Somente finalizadores marcados com <xref:System.EnterpriseServices.MustRunInClientContextAttribute> são executados. Da mesma forma, todos os threads com isso <xref:System.AppDomain> em sua pilha recebem um `ThreadAbortException` , mas somente os `catch` `finally` blocos e bloqueados com <xref:System.EnterpriseServices.MustRunInClientContextAttribute> são executados.|  
|`eThrowException`|Especifica que uma exceção apropriada para a condição, como memória insuficiente, estouro de buffer e assim por diante, deve ser lançada.|  
|`eUnloadAppDomain`|Especifica que o <xref:System.AppDomain> deve ser descarregado. O CLR tenta executar finalizadores.|  
  
## <a name="remarks"></a>Comentários  

 O host define as ações de política chamando métodos da interface [ICLRPolicyManager](iclrpolicymanager-interface.md) . Para obter informações sobre anulações rudes e normais, consulte a enumeração [EClrOperation](eclroperation-enumeration.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração EClrFailure](eclrfailure-enumeration.md)
- [Interface ICLRPolicyManager](iclrpolicymanager-interface.md)
- [Interface IHostPolicyManager](ihostpolicymanager-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
