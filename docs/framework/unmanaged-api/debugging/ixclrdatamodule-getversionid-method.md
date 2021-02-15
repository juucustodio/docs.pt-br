---
description: 'Saiba mais sobre o método: IXCLRDataModule:: getversionid'
title: 'Método IXCLRDataModule:: getversionid'
ms.date: 01/16/2019
api.name:
- IXCLRDataModule::GetVersionId Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataModule::GetVersionId Method
helpviewer.keywords:
- IXCLRDataModule::GetVersionId Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 1b924757f43d106df555ea028270ac873f8f4558
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800754"
---
# <a name="ixclrdatamodulegetversionid-method"></a>Método IXCLRDataModule:: getversionid

Obtém o identificador de versão do módulo.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetVersionId(
    [out] GUID* vid
);
```

## <a name="parameters"></a>Parâmetros

`vid`\
fora O identificador de versão do módulo.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da `IXCLRDataModule` interface e corresponde ao slot 41 ª da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** None  
**Biblioteca:** None  
**.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Interface IXCLRDataModule](ixclrdatamodule-interface.md)
