---
description: 'Saiba mais sobre o método: ICorDebugStepper:: SetRangeIL'
title: Método ICorDebugStepper::SetRangeIL
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.SetRangeIL
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::SetRangeIL
helpviewer_keywords:
- SetRangeIL method [.NET Framework debugging]
- ICorDebugStepper::SetRangeIL method [.NET Framework debugging]
ms.assetid: a20c95f0-6da7-4b41-b27f-584211cebb92
topic_type:
- apiref
ms.openlocfilehash: 8bccaf8ba8e52a7fe94555fa99b1c3cf92842efe
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717674"
---
# <a name="icordebugsteppersetrangeil-method"></a>Método ICorDebugStepper::SetRangeIL

Define um valor que especifica se as chamadas para [ICorDebugStepper:: StepRange](icordebugstepper-steprange-method.md) passam valores de argumentos que são relativos ao código nativo ou em relação ao código MSIL (Microsoft Intermediate Language) do método que está sendo percorrido.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetRangeIL (  
    [in] BOOL    bIL  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `bIL`  
 no Defina como `true` para especificar que os intervalos são relativos ao código MSIL. Defina como `false` para especificar que os intervalos são relativos ao código nativo. O valor padrão é `true`.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
