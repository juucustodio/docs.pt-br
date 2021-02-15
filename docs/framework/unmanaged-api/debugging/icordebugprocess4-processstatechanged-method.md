---
description: 'Saiba mais sobre: ICorDebugProcess4: método rocessStateChanged de:P'
title: 'ICorDebugProcess4: método rocessStateChanged de:P'
ms.date: 02/07/2019
api_name:
- ICorDebugProcess4::ProcessStateChanged
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess4::ProcessStateChanged
helpviewer_keywords:
- ICorDebugProcess4::ProcessStateChanged method [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 35a76b3c6dd9b37d3f06f23bc2ffea82f125a29e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746445"
---
# <a name="icordebugprocess4processstatechanged-method"></a>ICorDebugProcess4: método rocessStateChanged de:P

Notifica o pipeline ICorDebug que o depurador fora do processo está continuando a execução do depurador.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT ProcessStateChanged(
    [in] CorDebugStateChange change
);
```

## <a name="parameters"></a>Parâmetros

 `eChange`\
no Um membro da [Enumeração CorDebugStateChange](cordebugstatechange-enumeration.md) que descreve uma alteração no estado de execução do processo.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da `ICorDebugProcess4` interface e corresponde ao quarto slot da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

 **Cabeçalho:** None

 **Biblioteca:** None

 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Interface ICorDebugProcess4](icordebugprocess4-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
