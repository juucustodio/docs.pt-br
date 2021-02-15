---
description: 'Saiba mais sobre o método: IXCLRDataMethodInstance:: GetILAddressMap'
title: 'Método IXCLRDataMethodInstance:: GetILAddressMap'
ms.date: 01/16/2019
api.name:
- IXCLRDataMethodInstance::GetILAddressMap Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodInstance::GetILAddressMap Method
helpviewer.keywords:
- IXCLRDataMethodInstance::GetILAddressMap Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: ddddf593c3c18f2b4cd1682b5d6f7c8ff1985ac6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800806"
---
# <a name="ixclrdatamethodinstancegetiladdressmap-method"></a>Método IXCLRDataMethodInstance:: GetILAddressMap

Obtém o IL para endereçar informações de mapeamento.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetILAddressMap(
    [in] ULONG32                                   mapLen,
    [out] ULONG32                                 *mapNeeded,
    [out, size_is(mapLen)] CLRDATA_IL_ADDRESS_MAP  maps[]
);
```

## <a name="parameters"></a>Parâmetros

`mapLen`\
no O comprimento da matriz de mapas fornecida.

`mapNeeded`\
fora O número de entradas de mapa que o método precisa.

`maps`\
[fora, size_is (Bordon)] A matriz para armazenar as entradas do mapa.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da `IXCLRDataMethodInstance` interface e corresponde ao décimo quinto slot da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Interface IXCLRDataMethodInstance](ixclrdatamethodinstance-interface.md)
