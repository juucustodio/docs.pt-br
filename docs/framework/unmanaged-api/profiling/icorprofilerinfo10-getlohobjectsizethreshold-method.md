---
description: 'Saiba mais sobre o método: ICorProfilerInfo10:: GetLOHObjectSizeThreshold'
title: ICorProfilerInfo10::GetLOHObjectSizeThreshold
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo10.GetLOHObjectSizeThreshold
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 665a08ae226f04d5282b9584932078736751d5d0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737301"
---
# <a name="icorprofilerinfo10getlohobjectsizethreshold-method"></a>Método ICorProfilerInfo10:: GetLOHObjectSizeThreshold

Obtém o valor do limite de LOH (heap de objeto grande) configurado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetLOHObjectSizeThreshold( [out] DWORD *pThreshold );
```

## <a name="parameters"></a>Parâmetros

- `pThreshold`

  \[out] o limite de heap de objeto grande em bytes.

## <a name="remarks"></a>Comentários

Os objetos maiores que o limite de heap de objeto grande serão alocados no heap de objeto grande. A partir do .NET Core 3,0, o limite de heap de objeto grande é configurável, conterá `pThreshold` o tamanho limite de heap de objeto grande ativo em bytes.

## <a name="requirements"></a>Requisitos

**Plataformas:** Consulte [sistemas operacionais com suporte do .NET Core](../../../core/install/windows.md?pivots=os-windows).

**Cabeçalho:** CorProf. idl, CorProf. h

**Biblioteca:** CorGuids.lib

**Versões do .net:**[!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]

## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo10](icorprofilerinfo10-interface.md)
