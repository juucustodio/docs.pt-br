---
description: 'Saiba mais sobre: ICorDebugStepper: método eactivate de:D'
title: Método ICorDebugStepper::Deactivate
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.Deactivate
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::Deactivate
helpviewer_keywords:
- Deactivate method [.NET Framework debugging]
- ICorDebugStepper::Deactivate method [.NET Framework debugging]
ms.assetid: 855f4199-b62d-40ce-998e-1eb4a1772142
topic_type:
- apiref
ms.openlocfilehash: 039c52f5bc237506dcc648ace70789c8eb7ef8c9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794657"
---
# <a name="icordebugstepperdeactivate-method"></a>Método ICorDebugStepper::Deactivate

Faz com que esse ICorDebugStepper cancele o comando da última etapa que ele recebeu.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Deactivate ();  
```  
  
## <a name="remarks"></a>Comentários  

 Um novo comando de revisão pode ser emitido depois que o comando de etapa recebido mais recentemente tiver sido cancelado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
