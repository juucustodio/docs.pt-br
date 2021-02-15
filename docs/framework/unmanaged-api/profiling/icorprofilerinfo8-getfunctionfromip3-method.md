---
description: 'Saiba mais sobre o método: ICorProfilerInfo8:: GetFunctionFromIP3'
title: ICorProfilerInfo8::GetFunctionFromIP3
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo8.GetFunctionFromIP3
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 3ce0a0964e26254ab09e515826b6bceb657e07bc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783827"
---
# <a name="icorprofilerinfo8getfunctionfromip3-method"></a>Método ICorProfilerInfo8:: GetFunctionFromIP3

Mapeia um ponteiro de instrução de código gerenciado para uma FunctionID. Esse método funciona para métodos dinâmicos e não dinâmicos.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetFunctionFromIP3([in] LPCBYTE ip,
                           [out] FunctionID *functionId,
                           [out] ReJITID * pReJitId);
```

## <a name="parameters"></a>Parâmetros

- `ip`

  \[in] o ponteiro de instrução no código gerenciado.

- `pFunctionId`

  \[out] a ID da função.

- `pReJitId`

  \[out] a identidade da versão recompilada do JIT da função.

## <a name="remarks"></a>Comentários

Esse método funciona para métodos dinâmicos e não dinâmicos. É um superconjunto de [GetFunctionFromIP2](icorprofilerinfo4-getfunctionfromip2-method.md), que funciona apenas para funções com metadados.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorProf. idl, CorProf. h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo8](icorprofilerinfo8-interface.md)
