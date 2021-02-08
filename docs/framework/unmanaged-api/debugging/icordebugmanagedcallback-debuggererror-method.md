---
description: 'Saiba mais sobre: ICorDebugManagedCallback: método ebuggerError de:D'
title: Método ICorDebugManagedCallback::DebuggerError
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.DebuggerError
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::DebuggerError
helpviewer_keywords:
- DebuggerError method [.NET Framework debugging]
- ICorDebugManagedCallback::DebuggerError method [.NET Framework debugging]
ms.assetid: 9e983d11-eaf3-4741-b936-29ec456384a3
topic_type:
- apiref
ms.openlocfilehash: 2f73e07711f7d2ce865aab8f90862563e767fd16
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790991"
---
# <a name="icordebugmanagedcallbackdebuggererror-method"></a>Método ICorDebugManagedCallback::DebuggerError

Notifica o depurador de que ocorreu um erro ao tentar lidar com um evento do Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DebuggerError (  
    [in] ICorDebugProcess *pProcess,  
    [in] HRESULT           errorHR,  
    [in] DWORD             errorCode  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pProcess`  
 no Um ponteiro para um objeto "ICorDebugProcess" que representa o processo no qual o evento ocorreu.  
  
 `errorHR`  
 no O valor HRESULT que foi retornado do manipulador de eventos.  
  
 `errorCode`  
 no Um inteiro que especifica o erro CLR.  
  
## <a name="remarks"></a>Comentários  

 O processo pode ser colocado em modo de passagem, dependendo da natureza do erro.  
  
 O `DebugError` retorno de chamada indica que os serviços de depuração foram desabilitados devido a um erro, portanto, os depuradores devem tornar a mensagem de erro disponível para o usuário. [ICorDebugProcess:: GetID](icordebugprocess-getid-method.md) será seguro chamar, mas todos os outros métodos, incluindo [ICorDebug:: Terminate](icordebug-terminate-method.md), não devem ser chamados. O depurador deve usar recursos do sistema operacional para encerrar processos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
