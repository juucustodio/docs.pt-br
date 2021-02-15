---
description: 'Saiba mais sobre o método: IXCLRDataProcess:: EndEnumMethodInstancesByAddress'
title: 'Método IXCLRDataProcess:: EndEnumMethodInstancesByAddress'
ms.date: 01/16/2019
api.name:
- IXCLRDataProcess::EndEnumMethodInstancesByAddress Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataProcess::EndEnumMethodInstancesByAddress Method
helpviewer.keywords:
- IXCLRDataProcess::EndEnumMethodInstancesByAddress Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 2e01fe0737319a7b336d9f6992bf81b2c57f9e70
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800715"
---
# <a name="ixclrdataprocessendenummethodinstancesbyaddress-method"></a>Método IXCLRDataProcess:: EndEnumMethodInstancesByAddress

Libera os recursos usados por iteradores internos usados durante a enumeração da instância.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EndEnumMethodInstancesByAddress(
    [in] CLRDATA_ENUM handle
);
```

## <a name="parameters"></a>Parâmetros

`handle`\
fora Um identificador para enumerar as instâncias de método.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da `IXCLRDataProcess` interface e corresponde ao slot 30 da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Enumeração CLRDataSourceType](clrdatasourcetype-enumeration.md)
- [Depuração](index.md)
- [Interface IXCLRDataProcess](ixclrdataprocess-interface.md)
