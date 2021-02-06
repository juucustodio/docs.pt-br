---
description: 'Saiba mais sobre: interface ICorDebugProcess4'
title: Interface ICorDebugProcess4
ms.date: 02/07/2019
api_name:
- ICorDebugProcess4
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess4
helpviewer_keywords:
- ICorDebugProcess4 interface [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 16c7f3fbd1a79b1406fe0c19a9d922964667a2a4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649982"
---
# <a name="icordebugprocess4-interface"></a>Interface ICorDebugProcess4

Fornece suporte para controle de execução fora do processo.

## <a name="methods"></a>Métodos

| Método                                                                 | Descrição                                                                                             |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| [ProcessStateChanged](icordebugprocess4-processstatechanged-method.md) | Notifica o pipeline ICorDebug que o depurador fora do processo está continuando a execução do depurador. |

## <a name="remarks"></a>Comentários

Essa interface reside dentro do tempo de execução e não é exposta por nenhum cabeçalho ou arquivo de biblioteca. No entanto, é uma interface COM que deriva de `IUnknown` com GUID `E930C679-78AF-4953-8AB7-B0AABF0F9F80` que pode ser obtido por meio dos mecanismos com usuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** None

**Biblioteca:** None

**.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
