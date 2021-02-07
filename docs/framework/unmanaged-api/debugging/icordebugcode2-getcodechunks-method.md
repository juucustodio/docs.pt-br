---
description: 'Saiba mais sobre o método: ICorDebugCode2:: GetCodeChunks'
title: Método ICorDebugCode2::GetCodeChunks
ms.date: 03/30/2017
api_name:
- ICorDebugCode2.GetCodeChunks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode2::GetCodeChunks
helpviewer_keywords:
- GetCodeChunks method [.NET Framework debugging]
- ICorDebugCode2::GetCodeChunks method [.NET Framework debugging]
ms.assetid: 210a2f02-2678-4555-bc4a-78a0408764c8
topic_type:
- apiref
ms.openlocfilehash: 371d077466ff2390293d9d4e320d4c95a992fe54
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764951"
---
# <a name="icordebugcode2getcodechunks-method"></a>Método ICorDebugCode2::GetCodeChunks

Obtém as partes de código das quais este objeto de código é composto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCodeChunks (
    [in]  ULONG32     cbufSize,
    [out] ULONG32     *pcnumChunks,
    [out, size_is(cbufSize), length_is(*pcnumChunks)]
        CodeChunkInfo chunks[]
);
```

## <a name="parameters"></a>Parâmetros

`cbufSize`  
no Tamanho da `chunks` matriz.

`pcnumChunks`  
fora O número de partes retornadas na `chunks` matriz.

`chunks`  
fora Uma matriz de estruturas "CodeChunkInfo", cada uma representando uma única parte do código. Se o valor de `cbufSize` for 0, esse parâmetro poderá ser nulo.

## <a name="remarks"></a>Comentários

Os trechos de código nunca serão sobrepostos e eles seguirão a ordem em que seriam concatenados por [ICorDebugCode:: GetCode](icordebugcode-getcode-method.md). Um objeto de código MSIL (Microsoft Intermediate Language) no .NET Framework versão 2,0 incluirá uma única parte de código.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorDebug.idl, CorDebug.h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
