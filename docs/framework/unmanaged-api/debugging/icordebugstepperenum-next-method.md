---
description: 'Saiba mais sobre: ICorDebugStepperEnum:: Next Method'
title: Método ICorDebugStepperEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugStepperEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepperEnum::Next
helpviewer_keywords:
- Next method, ICorDebugStepperEnum interface [.NET Framework debugging]
- ICorDebugStepperEnum::Next method [.NET Framework debugging]
ms.assetid: d0ea0f30-e8d2-48b0-8477-e1a029ceb4dd
topic_type:
- apiref
ms.openlocfilehash: e0c17fbc570d5ea8a4a56c89a5a2c855ed045bd7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717427"
---
# <a name="icordebugstepperenumnext-method"></a>Método ICorDebugStepperEnum::Next

Obtém o número especificado de instâncias de ICorDebugStepper da enumeração, começando na posição atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next(  
    [in] ULONG  celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugStepper *steppers[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 no O número de `ICorDebugStepper` instâncias a serem recuperadas.  
  
 `steppers`  
 fora Uma matriz de ponteiros, cada um dos quais aponta para um `ICorDebugStepper` objeto.  
  
 `pceltFetched`  
 fora Aponta para o número de `ICorDebugStepper` instâncias realmente retornadas. Esse valor pode ser nulo se `celt` for um.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
