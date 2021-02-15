---
description: 'Saiba mais sobre o método: ICorProfilerInfo9:: GetILToNativeMapping3'
title: ICorProfilerInfo9::GetILToNativeMapping3
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo9.GetILToNativeMapping3
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 867375d57f9d166ed08bf68ada81fb5cdbb8afe3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646511"
---
# <a name="icorprofilerinfo9getiltonativemapping3-method"></a>Método ICorProfilerInfo9:: GetILToNativeMapping3

Dado o endereço de início do código nativo, retorna as informações de mapeamento nativo para IL para essa versão JIT do código.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetILToNativeMapping3( [in]  UINT_PTR pNativeCodeStartAddress,
                               [in]  ULONG32 cMap,
                               [out] ULONG32 *pcMap,
                               [out] COR_DEBUG_IL_TO_NATIVE_MAP map[]);
```

## <a name="parameters"></a>Parâmetros

- `pNativeCodeStartAddress`

  \[in] um ponteiro para o início de uma função nativa.

- `cMap`

  \[in] o tamanho máximo da `map` matriz.

- `pcMap`

  \[out] o número total de estruturas de COR_DEBUG_IL_TO_NATIVE_MAP disponíveis.

- `map`

  \[out] uma matriz de estruturas [COR_DEBUG_IL_TO_NATIVE_MAP](../debugging/cor-debug-il-to-native-map-structure.md) , cada uma delas especifica os deslocamentos. Depois que o `GetILToNativeMapping3` método retornar, `map` conterá algumas ou todas as `COR_DEBUG_IL_TO_NATIVE_MAP` estruturas.

## <a name="remarks"></a>Comentários

Quando a compilação em camadas está habilitada, um método pode ter mais de um corpo de código nativo. [ICorProfilerInfo9:: GetNativeCodeStartAddresses](icorprofilerinfo9-getnativecodestartaddresses-method.md) retornará os endereços iniciais para todos os corpos de código nativos.

## <a name="requirements"></a>Requisitos

**Plataformas:** Consulte [sistemas operacionais com suporte do .NET Core](../../../core/install/windows.md?pivots=os-windows).

**Cabeçalho:** CorProf. idl, CorProf. h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_core_22](../../../../includes/net-core-22-md.md)]

## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo9](icorprofilerinfo9-interface.md)
