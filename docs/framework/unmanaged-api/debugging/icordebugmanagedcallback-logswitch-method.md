---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback:: LogSwitch'
title: Método ICorDebugManagedCallback::LogSwitch
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.LogSwitch
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::LogSwitch
helpviewer_keywords:
- LogSwitch method [.NET Framework debugging]
- ICorDebugManagedCallback::LogSwitch method [.NET Framework debugging]
ms.assetid: 0ac59d27-783f-4a87-b7a8-baa3ccc54582
topic_type:
- apiref
ms.openlocfilehash: 658b2afbe7074062910670c6748dc579973715f8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99660460"
---
# <a name="icordebugmanagedcallbacklogswitch-method"></a>Método ICorDebugManagedCallback::LogSwitch

Notifica o depurador de que um thread gerenciado Common Language Runtime (CLR) chamou um método na <xref:System.Diagnostics.Switch> classe para criar, modificar ou excluir uma opção de depuração/rastreamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT LogSwitch (  
    [in] ICorDebugAppDomain  *pAppDomain,  
    [in] ICorDebugThread     *pThread,  
    [in] LONG                 lLevel,  
    [in] ULONG                ulReason,  
    [in] WCHAR               *pLogSwitchName,  
    [in] WCHAR               *pParentName);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `PAppDomain`  
 no Um ponteiro para um objeto ICorDebugAppDomain que representa o domínio do aplicativo que contém o thread gerenciado que criou, modificou ou excluiu uma opção de depuração/rastreamento.  
  
 `pThread`  
 no Um ponteiro para um objeto ICorDebugThread que representa o thread gerenciado.  
  
 `lLevel`  
 no Um valor que indica o nível de severidade da mensagem descritiva que foi gravada no log de eventos.  
  
 `ulReason`  
 no Um valor da enumeração [LogSwitchCallReason](logswitchcallreason-enumeration.md) que indica a operação executada na opção de depuração/rastreamento.  
  
 `pLogSwitchName`  
 no Um ponteiro para o nome da opção de depuração/rastreamento.  
  
 `pParentName`  
 no Um ponteiro para o nome do pai da opção de depuração/rastreamento.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
