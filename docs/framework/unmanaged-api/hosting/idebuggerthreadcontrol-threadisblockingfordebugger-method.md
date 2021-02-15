---
description: 'Saiba mais sobre o método: IDebuggerThreadControl:: ThreadIsBlockingForDebugger'
title: Método IDebuggerThreadControl::ThreadIsBlockingForDebugger
ms.date: 03/30/2017
api_name:
- IDebuggerThreadControl.ThreadIsBlockingForDebugger
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ThreadIsBlockingForDebugger
helpviewer_keywords:
- ThreadIsBlockingForDebugger method [.NET Framework hosting]
- IDebuggerThreadControl::ThreadIsBlockingForDebugger method [.NET Framework hosting]
ms.assetid: d4d7cb2d-69da-48b3-879a-1a8a68c9bfa8
topic_type:
- apiref
ms.openlocfilehash: 0fa96b2e36ea6653e1698dd32fa1e73d223afb94
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789509"
---
# <a name="idebuggerthreadcontrolthreadisblockingfordebugger-method"></a>Método IDebuggerThreadControl::ThreadIsBlockingForDebugger

Notifica o host que o thread que está enviando esse retorno de chamada está prestes a ser bloqueado nos serviços de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ThreadIsBlockingForDebugger ( );  
```  
  
## <a name="remarks"></a>Comentários  

 O `ThreadIsBlockingForDebugger` método sempre será chamado em um thread de tempo de execução.  
  
 O `ThreadIsBlockingForDebugger` método dá ao host uma oportunidade de executar outra ação enquanto o thread é bloqueado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **Versões do .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IDebuggerThreadControl](idebuggerthreadcontrol-interface.md)
