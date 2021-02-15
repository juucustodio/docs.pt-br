---
description: 'Saiba mais sobre o método: ICorDebugModule2:: SetJMCStatus'
title: Método ICorDebugModule2::SetJMCStatus
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.SetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::SetJMCStatus
helpviewer_keywords:
- SetJMCStatus method, ICorDebugModule2 interface [.NET Framework debugging]
- ICorDebugModule2::SetJMCStatus method [.NET Framework debugging]
ms.assetid: 8c6d2089-4dbb-4715-b9e9-2a4491c8c9ce
topic_type:
- apiref
ms.openlocfilehash: 7d91d098c21eac39d18a0aa7c3d4fd795be509ae
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790796"
---
# <a name="icordebugmodule2setjmcstatus-method"></a>Método ICorDebugModule2::SetJMCStatus

Define o status de Apenas Meu Código (JMC) de todos os métodos de todas as classes nesse ICorDebugModule2 para o valor especificado, exceto aqueles na `pTokens` matriz, que ele define para o valor oposto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetJMCStatus (  
    [in] BOOL                        bIsJustMyCode,  
    [in] ULONG32                     cTokens,  
    [in, size_is(cTokens)] mdToken   pTokens[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `bIsJustMycode`  
 no Defina como `true` se o código deve ser depurado; caso contrário, defina como `false` .  
  
 `cTokens`  
 no O tamanho da `pTokens` matriz.  
  
 `pTokens`  
 no Uma matriz de `mdToken` valores, cada um dos quais se refere a um método que terá seu status JMC definido como! `bIsJustMycode` .  
  
## <a name="remarks"></a>Comentários  

 O status de JMC de cada método especificado na `pTokens` matriz é definido como o oposto do `bIsJustMycode` valor. O status de todos os outros métodos neste módulo é definido como o `bIsJustMycode` valor.  
  
 O `SetJMCStatus` método apaga todas as configurações de JMC anteriores neste módulo.  
  
 O `SetJMCStatus` método retornará um S_OK HRESULT se todas as funções tiverem sido definidas com êxito. Ele retornará um CORDBG_E_FUNCTION_NOT_DEBUGGABLE HRESULT se algumas funções marcadas `true` não forem depurável.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
