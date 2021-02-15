---
description: 'Saiba mais sobre: interface IXCLRDataMethodInstance'
title: Interface IXCLRDataMethodInstance
ms.date: 02/01/2019
api.name:
- IXCLRDataMethodInstance Interface
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodInstance Interface
helpviewer.keywords:
- IXCLRDataMethodInstance Interface [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 4e9ad57988420ff14b297c693c31c0dc5b3b181c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800780"
---
# <a name="ixclrdatamethodinstance-interface"></a>Interface IXCLRDataMethodInstance

Fornece métodos para consultar informações sobre uma instância de método.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="methods"></a>Métodos

| Método                                                                                                                  | Descrição                                 |
| ----------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| [GetILAddressMap](ixclrdatamethodinstance-getiladdressmap-method.md) | Obtém o IL para endereçar informações de mapeamento. |
| [GetRepresentativeEntryAddress](ixclrdatamethodinstance-getrepresentativeentryaddress-method.md) | Obtém o endereço de ponto de entrada mais representativo para a compilação nativa de todos os pontos de entrada possíveis para um método. |

## <a name="remarks"></a>Comentários

Essa interface reside dentro do tempo de execução e não é exposta por nenhum cabeçalho ou arquivo de biblioteca. No entanto, é uma interface COM que deriva de `IUnknown` com GUID `ECD73800-22CA-4b0d-AB55-E9BA7E6318A5` que pode ser obtido por meio dos mecanismos com usuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Depurando interfaces](debugging-interfaces.md)
