---
description: 'Saiba mais sobre: ICorDebugTypeEnum:: Next Method'
title: Método ICorDebugTypeEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugTypeEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugTypeEnum::Next
helpviewer_keywords:
- ICorDebugTypeEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugTypeEnum interface [.NET Framework debugging]
ms.assetid: d0fdeba3-c195-4ece-8caf-79b1f40025d2
topic_type:
- apiref
ms.openlocfilehash: 9260f5f2d1a2d6943a705f7e7ef1ead3d2924cdc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690579"
---
# <a name="icordebugtypeenumnext-method"></a>Método ICorDebugTypeEnum::Next

Obtém o número de instâncias "ICorDebugType" especificadas pelo `celt` da enumeração, começando na posição atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next (  
    [in]  ULONG  celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugType *values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 no O número de `ICorDebugType` instâncias a serem recuperadas.  
  
 `values`  
 fora Uma matriz de ponteiros, cada um dos quais aponta para um `ICorDebugType` objeto.  
  
 `pceltFetched`  
 fora Aponta para o número de `ICorDebugType` instâncias realmente retornadas. Esse valor pode ser nulo se `celt` for um.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Confira também
