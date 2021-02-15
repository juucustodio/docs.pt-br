---
description: 'Saiba mais sobre o método: IXCLRDataMethodInstance:: GetRepresentativeEntryAddress'
title: 'Método IXCLRDataMethodInstance:: GetRepresentativeEntryAddress'
ms.date: 02/01/2019
api.name:
- IXCLRDataMethodInstance::GetRepresentativeEntryAddress
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodInstance::GetRepresentativeEntryAddress
helpviewer.keywords:
- IXCLRDataMethodInstance::GetRepresentativeEntryAddress Method [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 21cc6c50ab460c0e3a3a92c11fcfe51d4a2a4606
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800793"
---
# <a name="ixclrdatamethodinstancegetrepresentativeentryaddress-method"></a>Método IXCLRDataMethodInstance:: GetRepresentativeEntryAddress

Obtém o endereço de ponto de entrada mais representativo para a compilação nativa de todos os pontos de entrada possíveis para um método.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetRepresentativeEntryAddress(
    [out] CLRDATA_ADDRESS* addr
);
```

## <a name="parameters"></a>Parâmetros

`addr`\
fora O endereço do ponto de entrada nativo mais representativo para o método.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da [ `IXCLRDataMethodInstance` interface](ixclrdatamethodinstance-interface.md) e corresponde ao slot 20 da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Interface IXCLRDataMethodInstance](ixclrdatamethodinstance-interface.md)
