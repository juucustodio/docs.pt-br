---
description: 'Saiba mais sobre: método ICorDebugEval:: IsActive'
title: Método ICorDebugEval::IsActive
ms.date: 03/30/2017
api_name:
- ICorDebugEval.IsActive
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::IsActive
helpviewer_keywords:
- IsActive method, ICorDebugEval interface [.NET Framework debugging]
- ICorDebugEval::IsActive method [.NET Framework debugging]
ms.assetid: bf2bba24-d278-43bd-b1c5-35680e748d3e
topic_type:
- apiref
ms.openlocfilehash: 2314814f8979f460063017ebdf46beb512417395
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99694039"
---
# <a name="icordebugevalisactive-method"></a>Método ICorDebugEval::IsActive

Obtém um valor que indica se este objeto ICorDebugEval está em execução no momento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsActive (  
    [out] BOOL              *pbActive  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbActive`  
 fora Ponteiro para um valor que indica se essa avaliação está ativa.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
