---
description: 'Saiba mais sobre: interface ISOSDacInterface'
title: Interface ISOSDacInterface
ms.date: 02/01/2019
api.name:
- ISOSDacInterface Interface
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- ISOSDacInterface Interface
helpviewer.keywords:
- ISOSDacInterface Interface [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: ddb99b7c6fca6870024f04933861d01e4b31ea9e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790393"
---
# <a name="isosdacinterface-interface"></a>Interface ISOSDacInterface

Fornece métodos auxiliares para acessar dados do `SOS` .

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="methods"></a>Métodos

| Método                                                                                                               | Descrição                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| [GetMethodDescData](isosdacinterface-getmethoddescdata-method.md) | Obtém os dados para o ponteiro MethodDesc fornecido. |
| [GetMethodDescPtrFromIP](isosdacinterface-getmethoddescptrfromip-method.md) | Recupera o ponteiro do MethodDesc correspondente ao método que contém o endereço de instrução nativo fornecido. |
| [GetModuleData](isosdacinterface-getmoduledata-method.md)| Busca os dados correspondentes ao módulo carregado em um determinado endereço. |

## <a name="remarks"></a>Comentários

Essa interface reside dentro do tempo de execução e não é exposta por nenhum cabeçalho ou arquivo de biblioteca. No entanto, é uma interface COM que deriva de `IUnknown` com GUID `436f00f2-b42a-4b9f-870c-e73db66ae930` que pode ser obtido por meio dos mecanismos com usuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Depurando interfaces](debugging-interfaces.md)
