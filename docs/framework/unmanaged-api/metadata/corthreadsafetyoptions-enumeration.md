---
description: 'Saiba mais sobre: Enumeração CorThreadSafetyOptions'
title: Enumeração CorThreadSafetyOptions
ms.date: 03/30/2017
api_name:
- CorThreadSafetyOptions
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorThreadSafetyOptions
helpviewer_keywords:
- CorThreadSafetyOptions enumeration [.NET Framework metadata]
ms.assetid: dae07d9b-df51-488c-b17e-52d6e48217bd
topic_type:
- apiref
ms.openlocfilehash: 7915bcf5e7b71fa84ea83642467c1600cd38712d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99707313"
---
# <a name="corthreadsafetyoptions-enumeration"></a>Enumeração CorThreadSafetyOptions

Especifica sinalizadores para selecionar opções para a segurança do thread.

## <a name="syntax"></a>Sintaxe

```cpp
typedef enum CorThreadSafetyOptions {
    MDThreadSafetyDefault       = 0x00000000,
    MDThreadSafetyOff           = 0x00000000,
    MDThreadSafetyOn            = 0x00000001,
} CorThreadSafetyOptions;
```

## <a name="members"></a>Membros

|Membro|DESCRIÇÃO|
|------------|-----------------|
|`MDThreadSafetyDefault`|Valor padrão. Mesmo que `MDThreadSafetyOff`.|
|`MDThreadSafetyOff`|Indica que um bloqueio de leitor/gravador não pode ser definido.|
|`MDThreadSafetyOn`|Indica que um bloqueio de leitor/gravador pode ser definido.|

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorHdr. h

**.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
