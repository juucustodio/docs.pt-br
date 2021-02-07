---
description: 'Saiba mais sobre o método: IDebuggerThreadControl:: StartBlockingForDebugger'
title: Método IDebuggerThreadControl::StartBlockingForDebugger
ms.date: 03/30/2017
api_name:
- IDebuggerThreadControl.StartBlockingForDebugger
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- StartBlockingForDebugger
helpviewer_keywords:
- IDebuggerThreadControl::StartBlockingForDebugger method [.NET Framework hosting]
- StartBlockingForDebugger method [.NET Framework hosting]
ms.assetid: 5c8f11b4-35d3-4c39-9bbd-58b896ba5ba6
topic_type:
- apiref
ms.openlocfilehash: 3e19817c4adbefd1dd70be047656b3fea261c389
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709666"
---
# <a name="idebuggerthreadcontrolstartblockingfordebugger-method"></a>Método IDebuggerThreadControl::StartBlockingForDebugger

Notifica o host de que os serviços de depuração estão prestes a começar a bloquear todos os threads.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT StartBlockingForDebugger (  
    [in] DWORD dwUnused  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwUnused`  
 no Reservado para uso futuro.  
  
## <a name="remarks"></a>Comentários  

 O `StartBlockingForDebugger` método pode ser chamado em um thread de tempo de execução.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IDebuggerThreadControl](idebuggerthreadcontrol-interface.md)
