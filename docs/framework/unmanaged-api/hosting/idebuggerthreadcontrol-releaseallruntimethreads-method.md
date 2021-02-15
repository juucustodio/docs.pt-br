---
description: 'Saiba mais sobre o método: IDebuggerThreadControl:: ReleaseAllRuntimeThreads'
title: Método IDebuggerThreadControl::ReleaseAllRuntimeThreads
ms.date: 03/30/2017
api_name:
- IDebuggerThreadControl.ReleaseAllRuntimeThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ReleaseAllRuntimeThreads
helpviewer_keywords:
- ReleaseAllRuntimeThreads method [.NET Framework hosting]
- IDebuggerThreadControl::ReleaseAllRuntimeThreads method [.NET Framework hosting]
ms.assetid: 1a2995ff-5f02-4b49-84dc-3a5f9cfd7d55
topic_type:
- apiref
ms.openlocfilehash: bf551ccc2ae5bde3333dc8e3957099590a494dd3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709718"
---
# <a name="idebuggerthreadcontrolreleaseallruntimethreads-method"></a>Método IDebuggerThreadControl::ReleaseAllRuntimeThreads

Notifica o host de que os serviços de depuração estão prestes a liberar todos os threads bloqueados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ReleaseAllRuntimeThreads ( );  
```  
  
## <a name="remarks"></a>Comentários  

 O `ReleaseAllRuntimeThreads` método nunca será chamado em um thread de tempo de execução. Se o host tiver um thread de tempo de execução bloqueado, ele deverá liberá-lo agora.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IDebuggerThreadControl](idebuggerthreadcontrol-interface.md)
