---
description: 'Saiba mais sobre: ICorDebugFrame:: método createfimr'
title: Método ICorDebugFrame::CreateStepper
ms.date: 03/30/2017
api_name:
- ICorDebugFrame.CreateStepper
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFrame::CreateStepper
helpviewer_keywords:
- ICorDebugFrame::CreateStepper method [.NET Framework debugging]
- CreateStepper method, ICorDebugFrame interface [.NET Framework debugging]
ms.assetid: 689e7f28-20c1-4d5c-9baa-17441cd63a88
topic_type:
- apiref
ms.openlocfilehash: 394418b89fd7a1c780a5bc33b97b8ef40bab8df2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99693090"
---
# <a name="icordebugframecreatestepper-method"></a>Método ICorDebugFrame::CreateStepper

Obtém um stepper que permite que o depurador execute operações de depuração relativas a esse ICorDebugFrame.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateStepper (  
    [out] ICorDebugStepper   **ppStepper  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppStepper`  
 fora Um ponteiro para o endereço de um objeto ICorDebugStepper que permite que o depurador execute operações de depuração relativas ao quadro atual.  
  
## <a name="remarks"></a>Comentários  

 Se o quadro não estiver ativo, o objeto stepper normalmente precisará retornar ao quadro antes da conclusão da etapa.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
