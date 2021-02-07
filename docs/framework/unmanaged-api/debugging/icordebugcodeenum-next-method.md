---
description: 'Saiba mais sobre: ICorDebugCodeEnum:: Next Method'
title: Método ICorDebugCodeEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugCodeEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCodeEnum::Next
helpviewer_keywords:
- ICorDebugCodeEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugEnum interface [.NET Framework debugging]
ms.assetid: 644ece86-384d-4c63-9fba-52c789616ff7
topic_type:
- apiref
ms.openlocfilehash: 51d46718891ce3df537c675175eacc4e33b92f79
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764736"
---
# <a name="icordebugcodeenumnext-method"></a>Método ICorDebugCodeEnum::Next

Obtém o número especificado de instâncias "ICorDebugCode" da enumeração, começando na posição atual.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Next (
    [in] ULONG  celt,
    [out, size_is(celt), length_is(*pceltFetched)]
        ICorDebugCode *values[],
    [out] ULONG *pceltFetched
);
```

## <a name="parameters"></a>Parâmetros

`celt`  
no O número de `ICorDebugCode` instâncias a serem recuperadas.

`values`  
fora Uma matriz de ponteiros, cada um dos quais aponta para um `ICorDebugCode` objeto.

`pceltFetched`  
fora Um ponteiro para o número de `ICorDebugCode` instâncias retornadas de fato. Esse valor pode ser nulo se `celt` for um.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorDebug.idl, CorDebug.h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
