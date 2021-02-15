---
description: 'Saiba mais sobre o método: ICorDebugEval:: CallFunction'
title: Método ICorDebugEval::CallFunction
ms.date: 03/30/2017
api_name:
- ICorDebugEval.CallFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::CallFunction
helpviewer_keywords:
- ICorDebugEval::CallFunction method [.NET Framework debugging]
- CallFunction method [.NET Framework debugging]
ms.assetid: 7f470c5c-e1c0-4d8d-aad8-830f113ae751
topic_type:
- apiref
ms.openlocfilehash: c0978ab3bdffc83e3eb5e3a6553e7f374ab6d5da
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99694182"
---
# <a name="icordebugevalcallfunction-method"></a>Método ICorDebugEval::CallFunction

Define uma chamada para a função especificada.

Esse método é obsoleto no .NET Framework versão 2,0. Use [ICorDebugEval2:: CallParameterizedFunction](icordebugeval2-callparameterizedfunction-method.md) em vez disso.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CallFunction (
    [in] ICorDebugFunction  *pFunction,
    [in] ULONG32            nArgs,
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]
);
```

## <a name="parameters"></a>Parâmetros

`pFunction`\
no Ponteiro para um objeto ICorDebugFunction que especifica a função a ser chamada.

`nArgs`\
no O número de argumentos para a função.

`ppArgs`\
no Uma matriz de ponteiros, cada um dos quais aponta para um objeto ICorDebugValue que especifica um argumento a ser passado para a função.

## <a name="remarks"></a>Comentários

Se a função for virtual, `CallFunction` executará o despacho virtual. Se a função estiver em um domínio de aplicativo diferente, uma transição ocorrerá contanto que todos os argumentos também estejam nesse domínio de aplicativo.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorDebug.idl, CorDebug.h

**Biblioteca:** CorGuids.lib

**Versões do .NET Framework:** 1,1, 1,0

## <a name="see-also"></a>Consulte também

- [Método CallParameterizedFunction](icordebugeval2-callparameterizedfunction-method.md)
