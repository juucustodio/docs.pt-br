---
description: 'Saiba mais sobre: Enumeração CorDebugStateChange'
title: Enumeração CorDebugStateChange
ms.date: 02/07/2019
api_name:
- CorDebugStateChange
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 1d4424ab-5143-4e50-a84a-ceeb4ddf3bba
topic_type:
- apiref
ms.openlocfilehash: 1900baa77432daa10d0f1a32dd9cb25198b86ed1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661807"
---
# <a name="cordebugstatechange-enumeration"></a>Enumeração CorDebugStateChange

Descreve a quantidade de dados armazenados em cache que devem ser descartados com base em alterações no processo.

## <a name="syntax"></a>Sintaxe

```cpp
typedef enum CorDebugStateChange
{
    PROCESS_RUNNING = 0x0000001,
    FLUSH_ALL       = 0x0000002,
} CorDebugStateChange;
```

## <a name="members"></a>Membros

| Membro            | DESCRIÇÃO                                                              |
| ----------------- | ------------------------------------------------------------------------ |
| `PROCESS_RUNNING` | O processo atingiu um novo estado de memória por meio da execução do encaminhamento.            |
| `FLUSH_ALL`       | A memória do processo pode ser arbitrariamente diferente do que era anteriormente. |

## <a name="remarks"></a>Comentários

 Um membro da `CorDebugStateChange` enumeração é fornecido como um argumento quando o depurador chama o `ProcessStateChanged` método com [ICorDebugProcess4::P rocessstatechanged](icordebugprocess4-processstatechanged-method.md) ou [ICorDebugProcess6::P rocessstatechanged](icordebugprocess6-processstatechanged-method.md)

## <a name="requirements"></a>Requisitos

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

 **Cabeçalho:** CorDebug.idl, CorDebug.h

 **Biblioteca:** CorGuids.lib

 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
- [Depuração](index.md)
