---
description: 'Saiba mais sobre: Enumeração EMemoryCriticalLevel'
title: Enumeração EMemoryCriticalLevel
ms.date: 03/30/2017
api_name:
- EMemoryCriticalLevel
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EMemoryCriticalLevel
helpviewer_keywords:
- EMemoryCriticalLevel enumeration [.NET Framework hosting]
ms.assetid: 2ca8a7a2-7b54-4ba3-8e73-277c7df485f3
topic_type:
- apiref
ms.openlocfilehash: 88965a29164de1ec7b01c2fcc8f51415127e69fd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785426"
---
# <a name="ememorycriticallevel-enumeration"></a>Enumeração EMemoryCriticalLevel

Contém valores que indicam o impacto de uma falha quando uma alocação de memória específica é solicitada, mas não pode ser satisfeita.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    eTaskCritical      = 0,  
    eAppDomainCritical = 1,  
    eProcessCritical   = 2  
} EMemoryCriticalLevel;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`eAppDomainCritical`|Indica que a alocação é essencial para executar código gerenciado no domínio que solicitou a alocação. Se não for possível alocar memória, o CLR não poderá garantir que o domínio ainda seja utilizável. O host decide a ação a ser tomada quando a alocação não puder ser satisfeita. Ele pode instruir o CLR a anular o `AppDomain` automaticamente ou permitir que ele continue em execução chamando métodos em [ICLRPolicyManager](iclrpolicymanager-interface.md).|  
|`eProcessCritical`|Indica que a alocação é essencial para a execução do código gerenciado no processo. Esse valor é usado durante a inicialização e ao executar finalizadores. Se não for possível alocar memória, o CLR não poderá operar no processo. Se a alocação falhar, o CLR será efetivamente desabilitado. Todas as chamadas subsequentes para o CLR falham com HOST_E_CLRNOTAVAILABLE.|  
|`eTaskCritical`|Indica que a alocação é essencial para executar a tarefa que solicitou a alocação. Se não for possível alocar memória, o CLR não poderá garantir que a tarefa possa ser executada. Em caso de falha, o CLR gera um <xref:System.Threading.ThreadAbortException> no thread do sistema de operação física.|  
  
## <a name="remarks"></a>Comentários  

 Os métodos de alocação de memória definidos nas interfaces [IHostMemoryManager](ihostmemorymanager-interface.md) e [IHostMAlloc](ihostmalloc-interface.md) usam um parâmetro desse tipo. Dependendo da severidade de uma falha, um host pode decidir se a solicitação de alocação deve falhar imediatamente ou aguardar até que possa ser satisfeita.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRMemoryNotificationCallback](iclrmemorynotificationcallback-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
