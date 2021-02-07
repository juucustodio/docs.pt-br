---
description: 'Saiba mais sobre o método: ICorDebugModule2:: ResolveAssembly'
title: Método ICorDebugModule2::ResolveAssembly
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.ResolveAssembly
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::ResolveAssembly
helpviewer_keywords:
- ICorDebugModule2::ResolveAssembly method [.NET Framework debugging]
- ResolveAssembly method [.NET Framework debugging]
ms.assetid: ddf9085c-7161-44bd-9609-cd2732b9009f
topic_type:
- apiref
ms.openlocfilehash: fba53b8ff76e4d3deb1876d2a20a7a2edc20bd06
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99722588"
---
# <a name="icordebugmodule2resolveassembly-method"></a>Método ICorDebugModule2::ResolveAssembly

Resolve o assembly referenciado pelo token de metadados especificado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT ResolveAssembly (
    [in]  mdToken             tkAssemblyRef,
    [out] ICorDebugAssembly   **ppAssembly
);
```

## <a name="parameters"></a>Parâmetros

`tkAssemblyRef`\
no Um `mdToken` valor que faz referência ao assembly.

`ppAssembly`\
fora Um ponteiro para o endereço de um objeto ICorDebugAssembly que representa o assembly.

## <a name="remarks"></a>Comentários

Se o assembly ainda não estiver carregado quando `ResolveAssembly` for chamado, um valor HRESULT de CORDBG_E_CANNOT_RESOLVE_ASSEMBLY será retornado.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorDebug.idl, CorDebug.h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
