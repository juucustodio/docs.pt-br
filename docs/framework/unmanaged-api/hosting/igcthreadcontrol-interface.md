---
description: 'Saiba mais sobre: interface IGCThreadControl'
title: Interface IGCThreadControl
ms.date: 03/30/2017
api_name:
- IGCThreadControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IGCThreadControl
helpviewer_keywords:
- IGCThreadControl interface [.NET Framework hosting]
ms.assetid: 3ff04d75-85ac-4df9-886d-dbaa037c0552
topic_type:
- apiref
ms.openlocfilehash: 07c76848668b1525f4ff45ba5de746beefe0e004
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709276"
---
# <a name="igcthreadcontrol-interface"></a>Interface IGCThreadControl

Fornece métodos para participar do agendamento de threads que, de outra forma, seriam bloqueados para uma coleta de lixo.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método SuspensionEnding](igcthreadcontrol-suspensionending-method.md)|Notifica o host de que o tempo de execução está retomando threads após uma coleta de lixo ou outra suspensão.|  
|[Método SuspensionStarting](igcthreadcontrol-suspensionstarting-method.md)|Notifica o host de que o tempo de execução está começando uma suspensão de thread para uma coleta de lixo ou outra suspensão.|  
|[Método ThreadIsBlockingForSuspension](igcthreadcontrol-threadisblockingforsuspension-method.md)|Notifica o host que o thread que está fazendo a chamada está prestes a bloquear, talvez para uma coleta de lixo ou outra suspensão.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de hospedagem](hosting-interfaces.md)
