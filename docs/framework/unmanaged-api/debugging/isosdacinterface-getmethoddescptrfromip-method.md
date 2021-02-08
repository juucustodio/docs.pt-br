---
description: 'Saiba mais sobre o método: ISOSDacInterface:: GetMethodDescPtrFromIP'
title: 'Método ISOSDacInterface:: GetMethodDescPtrFromIP'
ms.date: 02/01/2019
api.name:
- ISOSDacInterface::GetMethodDescPtrFromIP Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- ISOSDacInterface::GetMethodDescPtrFromIP Method
helpviewer.keywords:
- ISOSDacInterface::GetMethodDescPtrFromIP Method [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 8d7c7071b7b3fc520faea71c8d7792317745cfde
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790406"
---
# <a name="isosdacinterfacegetmethoddescptrfromip-method"></a>Método ISOSDacInterface:: GetMethodDescPtrFromIP

Recupera o ponteiro do MethodDesc correspondente ao método que contém o endereço de instrução nativo fornecido.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetMethodDescPtrFromIP(
    CLRDATA_ADDRESS ip,
    CLRDATA_ADDRESS * ppMD
);
```

## <a name="parameters"></a>Parâmetros

`ip`\
no Um endereço dentro do método em tempo de execução.

`ppMD`\
fora O endereço do `MethodDesc` para o método específico.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da [ `ISOSDacInterface` interface](isosdacinterface-interface.md) e corresponde ao slot 22 da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Interface ISOSDacInterface](isosdacinterface-interface.md)
