---
description: 'Saiba mais sobre: estrutura de CLRDATA_ADDRESS_RANGE'
title: Estrutura CLRDATA_ADDRESS_RANGE
ms.date: 01/16/2019
api.name:
- CLRDATA_ADDRESS_RANGE Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- CLRDATA_ADDRESS_RANGE Structure
helpviewer.keywords:
- CLRDATA_ADDRESS_RANGE Structure [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 5d671a08064781b71756efc3c753468e6769d4ce
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662332"
---
# <a name="clrdata_address_range-structure"></a>Estrutura CLRDATA_ADDRESS_RANGE

Define um intervalo de endereços.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct
{
    CLRDATA_ADDRESS startAddress;
    CLRDATA_ADDRESS endAddress;
} CLRDATA_ADDRESS_RANGE;
```

## <a name="members"></a>Membros

| Membro         | DESCRIÇÃO                     |
| -------------- | ------------------------------- |
| `startAddress` | O endereço inicial do intervalo. |
| `endAddress`   | O endereço final do intervalo.   |

## <a name="remarks"></a>Comentários

Essa estrutura reside dentro do tempo de execução e não é exposta por nenhum cabeçalho ou arquivo de biblioteca. Para usá-lo, defina a estrutura conforme especificado acima, em que `CLRDATA_ADDRESS` é um inteiro sem sinal de 64 bits.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Estruturas de depuração](debugging-structures.md)
