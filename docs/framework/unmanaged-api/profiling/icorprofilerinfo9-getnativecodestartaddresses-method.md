---
description: 'Saiba mais sobre o método: ICorProfilerInfo9:: GetNativeCodeStartAddresses'
title: ICorProfilerInfo9::GetNativeCodeStartAddresses
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo9.GetNativeCodeStartAddresses
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 1ca686cef4a45ebb9e05190fa790ed5300c0d816
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646485"
---
# <a name="icorprofilerinfo9getnativecodestartaddresses-method"></a>Método ICorProfilerInfo9:: GetNativeCodeStartAddresses

Dada uma FunctionID e rejitId, enumera o endereço inicial do código de início de todas as versões com compilação JIT desse código que existem atualmente.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetNativeCodeStartAddresses( [in]  FunctionID functionID,
                                     [in]  ReJITID reJitId,
                                     [in]  ULONG32 cCodeStartAddresses,
                                     [out] ULONG32 *pcCodeStartAddresses,
                                     [out] UINT_PTR codeStartAddresses[]);
```

## <a name="parameters"></a>Parâmetros

- `functionId`

  \[in] a ID da função cujos endereços de início de código nativo devem ser retornados.

- `reJitId`

  \[in] a identidade da função de compilação JIT recompilada.

- `cCodeStartAddresses`

  \[in] o tamanho máximo da `codeStartAddresses` matriz.

- `pcCodeStartAddresses`

  \[out] o número de endereços disponíveis.

- `codeStartAddresses`

  \[out] uma matriz de `UINT_PTR` , cada uma delas é o endereço inicial de um corpo nativo para a função especificada.

## <a name="remarks"></a>Comentários

Quando a compilação em camadas está habilitada, uma função pode ter mais de um corpo de código nativo.

## <a name="requirements"></a>Requisitos

**Plataformas:** Consulte [sistemas operacionais com suporte do .NET Core](../../../core/install/windows.md?pivots=os-windows).

**Cabeçalho:** CorProf. idl, CorProf. h

**Biblioteca:** CorGuids.lib

**Versões do .net:**[!INCLUDE[net_core_22](../../../../includes/net-core-22-md.md)]

## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo9](icorprofilerinfo9-interface.md)
