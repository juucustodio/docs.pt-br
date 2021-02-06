---
description: 'Saiba mais sobre o método: ICorDebugProcess2:: GetThreadForTaskID'
title: Método ICorDebugProcess2::GetThreadForTaskID
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.GetThreadForTaskID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::GetThreadForTaskID
helpviewer_keywords:
- ICorDebugProcess2::GetThreadForTaskId method [.NET Framework debugging]
- GetThreadForTaskID method [.NET Framework debugging]
ms.assetid: 32d54a5b-8ad3-405b-a1b9-0936a3b49d1e
topic_type:
- apiref
ms.openlocfilehash: aafb1223f6e2e73aae600fd482c76b84c57dae52
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650125"
---
# <a name="icordebugprocess2getthreadfortaskid-method"></a>Método ICorDebugProcess2::GetThreadForTaskID

Obtém o thread no qual a tarefa com o identificador especificado está em execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetThreadForTaskID (  
    [in]  TASKID            taskid,  
    [out] ICorDebugThread2  **ppThread  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `taskid`  
 no O identificador da tarefa.  
  
 `ppThread`  
 fora Um ponteiro para o endereço de um objeto ICorDebugThread2 que representa o thread a ser recuperado.  
  
## <a name="remarks"></a>Comentários  

 O host pode definir o identificador de tarefa usando o método [ICLRTask:: SetTaskIdentifier](../hosting/iclrtask-settaskidentifier-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
