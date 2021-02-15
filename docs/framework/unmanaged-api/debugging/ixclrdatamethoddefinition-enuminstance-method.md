---
description: 'Saiba mais sobre o método: IXCLRDataMethodDefinition:: EnumInstance'
title: 'Método IXCLRDataMethodDefinition:: EnumInstance'
ms.date: 01/16/2019
api.name:
- IXCLRDataMethodDefinition::EnumInstance Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodDefinition::EnumInstance Method
helpviewer.keywords:
- IXCLRDataMethodDefinition::EnumInstance Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 4038dc4706b8362acaf9c13abd9c7326cce376a2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790354"
---
# <a name="ixclrdatamethoddefinitionenuminstance-method"></a>Método IXCLRDataMethodDefinition:: EnumInstance

Enumera as instâncias desta definição de método.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumInstance(
    [in, out] CLRDATA_ENUM         *handle,
    [out] IXCLRDataMethodInstance **instance
);
```

## <a name="parameters"></a>Parâmetros

`handle`\
[entrada, saída] Um identificador para enumerar as instâncias.

`instance`\
fora A instância enumerada.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da `IXCLRDataMethodDefinition` interface e corresponde ao quarto slot da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Enumeração CLRDataSourceType](clrdatasourcetype-enumeration.md)
- [Depuração](index.md)
- [Interface IXCLRDataMethodDefinition](ixclrdatamethoddefinition-interface.md)
- [Interface IXCLRDataMethodInstance](ixclrdatamethodinstance-interface.md)
