---
description: 'Saiba mais sobre: método ICorDebugProcess:: GetThread'
title: Método ICorDebugProcess::GetThread
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetThread
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetThread
helpviewer_keywords:
- ICorDebugProcess::GetThread method [.NET Framework debugging]
- GetThread method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: a48261ed-700b-41c9-8cb4-18c526546603
topic_type:
- apiref
ms.openlocfilehash: bd636df50afd3f12901c1b48559c44ac6ad0cb81
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746886"
---
# <a name="icordebugprocessgetthread-method"></a>Método ICorDebugProcess::GetThread

Obtém o thread deste processo que tem a ID do thread do sistema operacional especificado (SO).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetThread(  
    [in] DWORD dwThreadId,  
    [out] ICorDebugThread **ppThread);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwThreadId`  
 no A ID de thread do sistema operacional do thread a ser recuperado.  
  
 `ppThread`  
 fora Um ponteiro para o endereço de um objeto ICorDebugThread que representa o thread.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
