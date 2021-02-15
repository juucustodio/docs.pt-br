---
description: 'Saiba mais sobre: ICorDebugThread:: método createfimr'
title: Método ICorDebugThread::CreateStepper
ms.date: 03/30/2017
api_name:
- ICorDebugThread.CreateStepper
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::CreateStepper
helpviewer_keywords:
- ICorDebugThread::CreateStepper method [.NET Framework debugging]
- CreateStepper method, ICorDebugThread interface [.NET Framework debugging]
ms.assetid: 4657443f-dd12-431b-a648-175c23f13c83
topic_type:
- apiref
ms.openlocfilehash: 378ce28281f4f284c36194f993a53598a9de3854
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659355"
---
# <a name="icordebugthreadcreatestepper-method"></a>Método ICorDebugThread::CreateStepper

Cria um objeto ICorDebugStepper que permite percorrer o quadro ativo desse ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateStepper (  
    [out] ICorDebugStepper **ppStepper  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppStepper`  
 fora Um ponteiro para o endereço de um `ICorDebugStepper` objeto que permite percorrer o quadro ativo desse thread.  
  
## <a name="remarks"></a>Comentários  

 O quadro ativo pode ser um código não gerenciado.  
  
 A `ICorDebugStepper` interface deve ser usada para executar a depuração real.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
