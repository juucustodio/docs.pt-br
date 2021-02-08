---
description: 'Saiba mais sobre: interface IXCLRDataMethodDefinition'
title: Interface IXCLRDataMethodDefinition
ms.date: 01/16/2019
api.name:
- IXCLRDataMethodDefinition Interface
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodDefinition Interface
helpviewer.keywords:
- IXCLRDataMethodDefinition Interface [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: d73246b42a0bfb982c87b04d5490e945f7caa745
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790341"
---
# <a name="ixclrdatamethoddefinition-interface"></a>Interface IXCLRDataMethodDefinition

Fornece métodos para consultar informações sobre uma definição de método.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="methods"></a>Métodos

Os métodos a seguir são alguns dos métodos disponíveis na interface.

| Método                                                                                                                          | Descrição                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [StartEnumInstances](ixclrdatamethoddefinition-startenuminstances-method.md) | Fornece um identificador para a enumeração de instâncias de método para um determinado `IXCLRDataAppDomain` . |
| [EnumInstance](ixclrdatamethoddefinition-enuminstance-method.md)             | Enumera as instâncias desta definição de método.                                         |
| [EndEnumInstances](ixclrdatamethoddefinition-endenuminstances-method.md)     | Libera os recursos usados por iteradores internos usados durante a enumeração da instância.         |

## <a name="remarks"></a>Comentários

Essa interface reside dentro do tempo de execução e não é exposta por nenhum cabeçalho ou arquivo de biblioteca. No entanto, é uma interface COM que deriva de `IUnknown` com GUID `AAF60008-FB2C-420b-8FB1-42D244A54A97` que pode ser obtido por meio dos mecanismos com usuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Depurando interfaces](debugging-interfaces.md)
