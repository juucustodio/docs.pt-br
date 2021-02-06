---
description: 'Saiba mais sobre o método: ICorDebugProcess2:: GetVersion'
title: Método ICorDebugProcess2::GetVersion
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.GetVersion
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::GetVersion
helpviewer_keywords:
- GetVersion method, ICorDebugProcess2 interface [.NET Framework debugging]
- ICorDebugProcess2::GetVersion method [.NET Framework debugging]
ms.assetid: e11d5a75-61d9-4548-aedf-79c26079bd17
topic_type:
- apiref
ms.openlocfilehash: 8472e811ea4df1f99fb4e27b55f3561fae0c8a21
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650074"
---
# <a name="icordebugprocess2getversion-method"></a>Método ICorDebugProcess2::GetVersion

Obtém o número de versão do Common Language Runtime (CLR) que está em execução neste processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetVersion (
    [out] COR_VERSION     *version
);
```

## <a name="parameters"></a>Parâmetros

`version`\
fora Um ponteiro para uma estrutura de COR_VERSION que armazena o número de versão do tempo de execução.

## <a name="remarks"></a>Comentários

O `GetVersion` método retornará um código de erro se nenhum tempo de execução tiver sido carregado no processo.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorDebug.idl, CorDebug.h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
