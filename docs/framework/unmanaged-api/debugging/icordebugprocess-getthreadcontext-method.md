---
description: 'Saiba mais sobre o método: ICorDebugProcess:: GetThreadContext'
title: Método ICorDebugProcess::GetThreadContext
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetThreadContext
helpviewer_keywords:
- ICorDebugProcess::GetThreadContext method [.NET Framework debugging]
- GetThreadContext method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: 5b132ef1-8d4b-4525-89b3-54123596c194
topic_type:
- apiref
ms.openlocfilehash: 4cb926183522548e924013580f207d1d0677a0d3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746861"
---
# <a name="icordebugprocessgetthreadcontext-method"></a>Método ICorDebugProcess::GetThreadContext

Obtém o contexto para o thread determinado neste processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetThreadContext(  
    [in] DWORD threadID,  
    [in] ULONG32 contextSize,  
    [in, out, length_is(contextSize), size_is(contextSize)]  
    BYTE context[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `threadID`  
 no A ID do thread para o qual recuperar o contexto.  
  
 `contextSize`  
 no O tamanho da `context` matriz.  
  
 `context`  
 [entrada, saída] Uma matriz de bytes que descreve o contexto do thread.  
  
 O contexto especifica a arquitetura do processador no qual o thread está sendo executado.  
  
## <a name="remarks"></a>Comentários  

 O depurador deve chamar esse método em vez do `GetThreadContext` método Win32, pois o thread pode realmente estar em um estado "seqüestrado", no qual seu contexto foi alterado temporariamente. Esse método deve ser usado somente quando um thread estiver em código nativo. Use [ICorDebugRegisterSet](icordebugregisterset-interface.md) para threads em código gerenciado.  
  
 Os dados retornados são uma estrutura de contexto para a plataforma atual. Assim como ocorre com o `GetThreadContext` método Win32, o chamador deve inicializar o `context` parâmetro antes de chamar esse método.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
