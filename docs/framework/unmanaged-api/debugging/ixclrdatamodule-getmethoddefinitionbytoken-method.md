---
description: 'Saiba mais sobre o método: IXCLRDataModule:: GetMethodDefinitionByToken'
title: 'Método IXCLRDataModule:: GetMethodDefinitionByToken'
ms.date: 01/16/2019
api.name:
- IXCLRDataModule::GetMethodDefinitionByToken Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataModule::GetMethodDefinitionByToken Method
helpviewer.keywords:
- IXCLRDataModule::GetMethodDefinitionByToken Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 1eb1187d09183bfff97324a8032d23cbf471f580
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800767"
---
# <a name="ixclrdatamodulegetmethoddefinitionbytoken-method"></a>Método IXCLRDataModule:: GetMethodDefinitionByToken

Obtém a definição do método correspondente a um determinado token de metadados.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetMethodDefinitionByToken(
    [in] mdMethodDef token,
    [out] IXCLRDataMethodDefinition** methodDefinition
);
```

## <a name="parameters"></a>Parâmetros

`token`\
no O token do método.

`methodDefinition`\
fora A definição do método.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da `IXCLRDataModule` interface e corresponde ao slot 26 da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Interface IXCLRDataModule](ixclrdatamodule-interface.md)
