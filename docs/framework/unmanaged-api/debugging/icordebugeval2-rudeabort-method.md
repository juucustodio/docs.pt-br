---
description: 'Saiba mais sobre o método: ICorDebugEval2:: RudeAbort'
title: Método ICorDebugEval2::RudeAbort
ms.date: 03/30/2017
api_name:
- ICorDebugEval2.RudeAbort
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2::RudeAbort
helpviewer_keywords:
- ICorDebugEval2::RudeAbort method [.NET Framework debugging]
- RudeAbort method, ICorDebugEval2 interface [.NET Framework debugging]
ms.assetid: 02468edf-d32b-4cb3-aaa8-3dd2abfc8b25
topic_type:
- apiref
ms.openlocfilehash: 2835fd635da007b5ee3f0e642b77f3954945f168
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99693506"
---
# <a name="icordebugeval2rudeabort-method"></a>Método ICorDebugEval2::RudeAbort

Anula a computação que `ICorDebugEval2` está executando no momento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT RudeAbort ();  
```  
  
## <a name="remarks"></a>Comentários  

 `RudeAbort` não libera os bloqueios que o avaliador mantém, portanto, deixa a sessão de depuração em um estado não seguro. Chame esse método com extrema cautela.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
