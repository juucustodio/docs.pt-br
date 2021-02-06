---
description: 'Saiba mais sobre: método EnumImportTypes'
title: Método EnumImportTypes
ms.date: 03/30/2017
api_name:
- EnumImportTypes
- IALink.EnumImportTypes
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- EnumImportTypes
helpviewer_keywords:
- EnumImportTypes method
ms.assetid: 83a0e4e7-ec06-40cb-9b63-700b9695bb04
topic_type:
- apiref
ms.openlocfilehash: 39570740f3560f5bfef8ba80b95c0eb2aca41f59
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638113"
---
# <a name="enumimporttypes-method"></a>Método EnumImportTypes

Enumera cada tipo em cada escopo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumImportTypes(
    HALINKENUM   hEnum,
    DWORD        dwMax,
    mdTypeDef    aTypeDefs[],
    DWORD*       pdwCount
) PURE;
```

## <a name="parameters"></a>Parâmetros

`hEnum`\
Identificador para o enumerador.

`dwMax`\
Número máximo de tipos a serem recuperados.

`aTypeDefs`\
Recebe tokens de tipo, sem exceder `dwMax` .

`pdwCount`\
Recebe o número real do tipo em `aTypeDefs` .

## <a name="return-value"></a>Valor retornado

Retorna S_OK se o método tiver sucesso.

## <a name="requirements"></a>Requisitos

Requer ALink. h

## <a name="see-also"></a>Consulte também

- [Interface IALink](ialink-interface.md)
- [Interface IALink2](ialink2-interface.md)
- [API do ALink](index.md)
