---
description: 'Saiba mais sobre o método: ICorProfilerInfo8:: GetDynamicFunctionInfo'
title: ICorProfilerInfo8::GetDynamicFunctionInfo
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo8.GetDynamicFunctionInfo
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 48c8dbe20ccafb3fb23e9e289f728d5e3370613a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646576"
---
# <a name="icorprofilerinfo8getdynamicfunctioninfo-method"></a>Método ICorProfilerInfo8:: GetDynamicFunctionInfo

Recupera informações sobre métodos dinâmicos.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDynamicFunctionInfo( [in]  FunctionID              functionId,
                                [out] ModuleID                *moduleId,
                                [out] PCCOR_SIGNATURE         *ppvSig,
                                [out] ULONG                   *pbSig,
                                [in]  ULONG                   cchName,
                                [out] ULONG                   *pcchName,
                                [out] WCHAR                   wszName[]);
```

## <a name="parameters"></a>Parâmetros

- `functionId`

  \[in] a ID da função para a qual recuperar informações.

- `moduleId`

  \[in] um ponteiro para o módulo no qual a classe pai da função é definida.

- `ppvSig`

  \[out] um ponteiro para a assinatura da função.

- `pbSig`

  \[out] um ponteiro para a contagem de bytes para a assinatura de função.

- `cchName`

  \[in] o tamanho máximo da `wszName` matriz.

- `pcchName`

  \[out] o número de caracteres na `wszName` matriz.

- `wszName`

  \[out] uma matriz de `WCHAR` que é o nome da função, se houver uma.

## <a name="remarks"></a>Comentários

Determinados métodos, como stubs IL ou LCG, não têm metadados associados que podem ser recuperados usando as APIs [IMetaDataImport](../metadata/imetadataimport-interface.md) e [IMetaDataImport2](../metadata/imetadataimport2-interface.md) . Esses métodos podem ser encontrados por infilers por meio de ponteiros de instrução ou ouvindo [ICorProfilerCallback8::D ynamicmethodjitcompilationstarted](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md).

Essa API pode ser usada para recuperar informações sobre métodos dinâmicos, incluindo um nome amigável, se disponível.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorProf. idl, CorProf. h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo8](icorprofilerinfo8-interface.md)
