---
description: 'Saiba mais sobre o método: ICorDebugThread:: GetActiveChain'
title: Método ICorDebugThread::GetActiveChain
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetActiveChain
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetActiveChain
helpviewer_keywords:
- ICorDebugThread::GetActiveChain method [.NET Framework debugging]
- GetActiveChain method [.NET Framework debugging]
ms.assetid: f50de1f7-40ef-4949-b542-1d9a61f7bfef
topic_type:
- apiref
ms.openlocfilehash: d9aff80801fa72a227a84b3b5216e3ffa72b0e24
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659260"
---
# <a name="icordebugthreadgetactivechain-method"></a>Método ICorDebugThread::GetActiveChain

Obtém um ponteiro de interface para a cadeia de pilha ativa (mais recente) neste objeto ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetActiveChain (  
    [out] ICorDebugChain **ppChain  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppChain`  
 fora Um ponteiro para o endereço de um objeto ICorDebugChain que representa a cadeia de pilha.  
  
## <a name="remarks"></a>Comentários  

 O `ppChain` parâmetro será NULL se nenhuma cadeia de pilha estiver ativa no momento.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
