---
description: 'Saiba mais sobre: ICorDebugThreadEnum:: Next Method'
title: Método ICorDebugThreadEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugThreadEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThreadEnum::Next
helpviewer_keywords:
- ICorDebugThreadEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugThreadEnum interface [.NET Framework debugging]
ms.assetid: f967c93d-9a7f-4aaf-99a1-a1317899ff3f
topic_type:
- apiref
ms.openlocfilehash: 2cfb651d65eaf0f5797444ea1bec587cebdde2f4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658419"
---
# <a name="icordebugthreadenumnext-method"></a>Método ICorDebugThreadEnum::Next

Obtém o número de instâncias ICorDebugThread especificadas da enumeração, começando na posição atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next (  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugThread *threads[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 no O número de `ICorDebugThread` instâncias a serem recuperadas.  
  
 `threads`  
 fora Uma matriz de ponteiros, cada um dos quais aponta para um `ICorDebugThread` objeto que representa um thread.  
  
 `pceltFetched`  
 fora Aponta para o número de `ICorDebugThread` instâncias realmente retornadas. Esse valor pode ser nulo se `celt` for um.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
