---
description: 'Saiba mais sobre: Enumeração EClrOperation'
title: Enumeração EClrOperation
ms.date: 03/30/2017
api_name:
- EClrOperation
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrOperation
helpviewer_keywords:
- EClrOperation enumeration [.NET Framework hosting]
ms.assetid: 5aef6808-5aac-4b2f-a2c7-fee1575c55ed
topic_type:
- apiref
ms.openlocfilehash: 9f75762a400955b5f36fb2a337f283e36a32658c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785556"
---
# <a name="eclroperation-enumeration"></a>Enumeração EClrOperation

Descreve o conjunto de operações para as quais um host pode aplicar ações de política.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    OPR_ThreadAbort,  
    OPR_ThreadRudeAbortInNonCriticalRegion,  
    OPR_ThreadRudeAbortInCriticalRegion,  
    OPR_AppDomainUnload,  
    OPR_AppDomainRudeUnload,  
    OPR_ProcessExit,  
    OPR_FinalizerRun  
} EClrOperation;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`OPR_AppDomainRudeUnload`|O host pode especificar ações de política a serem executadas quando um <xref:System.AppDomain> for descarregado em um modo não normal (rude).|  
|`OPR_AppDomainUnload`|O host pode especificar ações de política a serem executadas quando um <xref:System.AppDomain> for descarregado.|  
|`OPR_FinalizerRun`|O host pode especificar ações de política a serem executadas quando os finalizadores forem executados.|  
|`OPR_ProcessExit`|O host pode especificar ações de política a serem executadas quando o processo for encerrado.|  
|`OPR_ThreadAbort`|O host pode especificar ações de política a serem executadas quando um thread for anulado.|  
|`OPR_ThreadRudeAbortInCriticalRegion`|O host pode especificar ações de política a serem executadas quando uma anulação de thread rude ocorrer em uma região crítica de código.|  
|`OPR_ThreadRudeAbortInNonCriticalRegion`|O host pode especificar ações de política a serem executadas quando uma anulação de thread rude ocorrer em uma região não crítica de código.|  
  
## <a name="remarks"></a>Comentários  

 A infraestrutura de confiabilidade do Common Language Runtime (CLR) distingue entre anulações e falhas de alocação de recursos que ocorrem em regiões críticas de código e aquelas que ocorrem em regiões não críticas de código. Essa distinção foi projetada para permitir que os hosts definam políticas diferentes dependendo de onde ocorrer uma falha no código.  
  
 Uma *região crítica de código* é qualquer espaço em que o CLR não possa garantir que a anulação de uma tarefa ou a falha de concluir uma solicitação de recursos afetará apenas a tarefa atual. Por exemplo, se uma tarefa estiver mantendo um bloqueio e receber um HRESULT que indica falha ao fazer uma solicitação de alocação de memória, é insuficiente simplesmente anular essa tarefa para garantir a estabilidade do <xref:System.AppDomain> , pois o <xref:System.AppDomain> pode conter outras tarefas aguardando o mesmo bloqueio. Para abandonar, a tarefa atual pode fazer com que essas outras tarefas parem de responder. Nesse caso, o host precisa da capacidade de descarregar todo o <xref:System.AppDomain> risco em potencial de instabilidade.  
  
 Uma *região não-crítica de código*, por outro lado, é uma região em que o CLR pode garantir que uma anulação ou uma falha afete apenas a tarefa sobre a qual o erro ocorre.  
  
 O CLR também distingue entre anulações normais e não normais (rudes). Em geral, uma anulação normal ou regular faz cada esforço para executar rotinas de manipulação de exceção e finalizadores antes de abortar uma tarefa, enquanto uma anulação rude não faz nenhuma garantia.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração EClrFailure](eclrfailure-enumeration.md)
- [Enumeração EPolicyAction](epolicyaction-enumeration.md)
- [Interface ICLRPolicyManager](iclrpolicymanager-interface.md)
- [Interface IHostPolicyManager](ihostpolicymanager-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
