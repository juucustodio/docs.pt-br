---
description: 'Saiba mais sobre: Enumeração CLRDataSourceType'
title: Enumeração CLRDataSourceType
ms.date: 01/16/2019
api.name:
- CLRDataSourceType Enumeration
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- CLRDataSourceType Enumeration
helpviewer.keywords:
- CLRDataSourceType Enumeration [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 06590e21aa4cdf6e89977a79da36a413d5ff4f1c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99747235"
---
# <a name="clrdatasourcetype-enumeration"></a>Enumeração CLRDataSourceType

Fornece valores que são usados pela estrutura de CLRDATA_IL_ADDRESS_MAP.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
typedef enum
{
    CLRDATA_SOURCE_TYPE_INVALID        = 0x00, // To indicate that nothing else applies
} CLRDataSourceType;
```

## <a name="members"></a>Membros

| Membro                        | DESCRIÇÃO                           |
| ----------------------------- | ------------------------------------- |
| `CLRDATA_SOURCE_TYPE_INVALID` | Para indicar que nada mais se aplica |

## <a name="remarks"></a>Comentários

Essa enumeração reside dentro do tempo de execução e não é exposta por nenhum cabeçalho ou arquivo de biblioteca. Para usá-lo, defina uma enumeração conforme definido acima no seu código. Isso também é alias `CLRDATA_ENUM` como mencionado em tipos de [dados comuns](../common-data-types-unmanaged-api-reference.md).

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Declarando enumerações](debugging-enumerations.md)
