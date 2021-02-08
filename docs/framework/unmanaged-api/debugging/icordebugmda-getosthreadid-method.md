---
description: 'Saiba mais sobre o método: ICorDebugMDA:: GetOSThreadId'
title: Método ICorDebugMDA::GetOSThreadId
ms.date: 03/30/2017
api_name:
- ICorDebugMDA.GetOSThreadId
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA::GetOSThreadId
helpviewer_keywords:
- ICorDebugMDA::GetOSThreadId method [.NET Framework debugging]
- GetOSThreadId method [.NET Framework debugging]
ms.assetid: 7ca7c364-ade4-4219-b434-9f6ae2359be6
topic_type:
- apiref
ms.openlocfilehash: f965585a6e6060a14f0cbc2a80b46124b2751e0e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801144"
---
# <a name="icordebugmdagetosthreadid-method"></a>Método ICorDebugMDA::GetOSThreadId

Obtém o identificador de thread do sistema operacional no qual o MDA (Assistente de depuração gerenciada) representado por [ICorDebugMDA](icordebugmda-interface.md) está em execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetOSThreadId (  
    [out] DWORD    *pOsTid  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pOsTid`  
 fora Um ponteiro para o identificador de thread do sistema operacional.  
  
## <a name="remarks"></a>Comentários  

 O thread do sistema operacional é usado em vez de um ICorDebugThread para permitir situações em que um MDA seja acionado em um thread nativo ou em um thread gerenciado que ainda não tenha inserido código gerenciado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugMDA](icordebugmda-interface.md)
- [Diagnosticando erros com assistentes de depuração gerenciados](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
