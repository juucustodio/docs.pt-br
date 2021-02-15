---
description: 'Saiba mais sobre o método: ICorProfilerInfo9:: GetCodeInfo4'
title: ICorProfilerInfo9::GetCodeInfo4
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo9.GetCodeInfo4
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 765f3dfee6c56148eb7807b0606e79d4b3a2e7a1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783801"
---
# <a name="icorprofilerinfo9getcodeinfo4-method"></a>Método ICorProfilerInfo9:: GetCodeInfo4

Dado o endereço de início do código nativo, retorna os blocos de memória virtual que armazenam esse código.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCodeInfo4( [in]  UINT_PTR pNativeCodeStartAddress,
                      [in]  ULONG32 cCodeInfos,
                      [out] ULONG32* pcCodeInfos,
                      [out] COR_PRF_CODE_INFO codeInfos[]);
```

## <a name="parameters"></a>Parâmetros

- `pNativeCodeStartAddress`

  \[in] um ponteiro para o início de uma função nativa.

- `cCodeInfos`

  \[in] o tamanho da `codeInfos` matriz.

- `pcCodeInfos`

  \[out] um ponteiro para o número total de estruturas de [COR_PRF_CODE_INFO](cor-prf-code-info-structure.md) disponíveis.

- `codeInfos`

  \[out] um buffer fornecido pelo chamador. Depois que o método retorna, ele contém uma matriz de `COR_PRF_CODE_INFO` estruturas, cada uma delas descreve um bloco de código nativo.

## <a name="remarks"></a>Comentários

O `GetCodeInfo4` método é semelhante a [GetCodeInfo3](icorprofilerinfo4-getcodeinfo3-method.md), exceto pelo fato de que ele pode pesquisar informações de código para versões nativas diferentes de um método.

> [!NOTE]
> `GetCodeInfo4` pode disparar uma coleta de lixo.

As extensões são classificadas em ordem crescente de deslocamento de Common Intermediate Language (CIL).

Depois de `GetCodeInfo4` retornar, você deve verificar se o `codeInfos` buffer foi grande o suficiente para conter todas as estruturas de [COR_PRF_CODE_INFO](cor-prf-code-info-structure.md) . Para fazer isso, compare o valor de `cCodeInfos` com o valor do `cchName` parâmetro. Se `cCodeInfos` dividido pelo tamanho de uma estrutura de [COR_PRF_CODE_INFO](cor-prf-code-info-structure.md) for menor que `pcCodeInfos` , aloque um `codeInfos` buffer maior, atualize `cCodeInfos` com o tamanho novo, maior e chame `GetCodeInfo4` novamente.

Como alternativa, você pode primeiro chamar `GetCodeInfo4` com um buffer de comprimento zero `codeInfos` para obter o tamanho de buffer correto. Em seguida, você pode definir o `codeInfos` tamanho do buffer para o valor retornado em `pcCodeInfos` , multiplicado pelo tamanho de uma estrutura de [COR_PRF_CODE_INFO](cor-prf-code-info-structure.md) e chamar `GetCodeInfo4` novamente.

## <a name="requirements"></a>Requisitos

**Plataformas:** Consulte [sistemas operacionais com suporte do .NET Core](../../../core/install/windows.md?pivots=os-windows).

**Cabeçalho:** CorProf. idl, CorProf. h

**Biblioteca:** CorGuids.lib

**Versões do .net:**[!INCLUDE[net_core_22](../../../../includes/net-core-22-md.md)]

## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo9](ICorProfilerInfo9-interface.md)
