---
description: 'Saiba mais sobre o método: ICorDebugStepper2:: SetJMC'
title: Método ICorDebugStepper2::SetJMC
ms.date: 03/30/2017
api_name:
- ICorDebugStepper2.SetJMC
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper2::SetJMC
helpviewer_keywords:
- ICorDebugStepper2::SetJMC method [.NET Framework debugging]
- SetJMC method [.NET Framework debugging]
ms.assetid: f5cdc135-6db4-4b32-9dd1-260ec58b774f
topic_type:
- apiref
ms.openlocfilehash: 07178ab90bb392e64c9d8a8fddf961efbb268002
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717531"
---
# <a name="icordebugstepper2setjmc-method"></a>Método ICorDebugStepper2::SetJMC

Define um valor que especifica se este ICorDebugStepper etapas somente por meio de código que é criado pelo desenvolvedor de um aplicativo. Esse processo também é conhecido como depuração de apenas meu código (JMC).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetJMC (  
    [in] BOOL    fIsJMCStepper  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fIsJMCStepper`  
 no Defina como `true` Step somente por meio de código que é criado pelo desenvolvedor de um aplicativo; caso contrário, defina como `false` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
