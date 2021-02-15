---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback:: ExitAppDomain'
title: Método ICorDebugManagedCallback::ExitAppDomain
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.ExitAppDomain
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::ExitAppDomain
helpviewer_keywords:
- ICorDebugManagedCallback::ExitAppDomain method [.NET Framework debugging]
- ExitAppDomain method [.NET Framework debugging]
ms.assetid: d815486e-b3bd-4fe8-ba28-02abdb4d67ba
topic_type:
- apiref
ms.openlocfilehash: a08f29c6c4c8196b968118433c31afb715935aec
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803614"
---
# <a name="icordebugmanagedcallbackexitappdomain-method"></a>Método ICorDebugManagedCallback::ExitAppDomain

Notifica o depurador de que um domínio de aplicativo foi encerrado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ExitAppDomain (  
    [in] ICorDebugProcess   *pProcess,  
    [in] ICorDebugAppDomain *pAppDomain  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pProcess`  
 no Um ponteiro para um objeto ICorDebugProcess que representa o processo que contém o domínio de aplicativo fornecido.  
  
 `pAppDomain`  
 no Um ponteiro para um objeto ICorDebugAppDomain que representa o domínio do aplicativo que foi encerrado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
