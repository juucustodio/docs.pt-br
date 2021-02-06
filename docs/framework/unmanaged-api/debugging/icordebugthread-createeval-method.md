---
description: 'Saiba mais sobre o método: ICorDebugThread:: CreateEval'
title: Método ICorDebugThread::CreateEval
ms.date: 03/30/2017
api_name:
- ICorDebugThread.CreateEval
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::CreateEval
helpviewer_keywords:
- CreateEval method [.NET Framework debugging]
- ICorDebugThread::CreateEval method [.NET Framework debugging]
ms.assetid: 36605067-33d3-4579-9c72-fb0e551ab0f1
topic_type:
- apiref
ms.openlocfilehash: a789840e099a14b584e5713bee12f5c4b0717fe7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659381"
---
# <a name="icordebugthreadcreateeval-method"></a>Método ICorDebugThread::CreateEval

Cria um objeto ICorDebugEval que coleta e expõe a funcionalidade desse ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateEval (  
    [out] ICorDebugEval   **ppEval  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppEval`  
 fora Um ponteiro para o endereço de um `ICorDebugEval` objeto que coleta e expõe a funcionalidade desse thread.  
  
## <a name="remarks"></a>Comentários  

 O objeto de avaliação enviará por push uma nova cadeia no thread antes de fazer seu cálculo. Isso interrompe a computação que está sendo executada atualmente no thread até que a avaliação seja concluída.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
