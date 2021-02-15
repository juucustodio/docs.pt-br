---
description: 'Saiba mais sobre o método: IXCLRDataModule:: Request'
title: 'Método IXCLRDataModule:: Request'
ms.date: 01/16/2019
api.name:
- IXCLRDataModule::Request Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataModule::Request Method
helpviewer.keywords:
- IXCLRDataModule::Request Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 96f4153c58a228cfb22a5cd25a53b6e60fc4dfd1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800728"
---
# <a name="ixclrdatamodulerequest-method"></a>Método IXCLRDataModule:: Request

Solicitações para popular o buffer fornecido com os dados do módulo.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Request([in] ULONG32 reqCode,
    [in] ULONG32 inBufferSize,
    [in, size_is(inBufferSize)] BYTE* inBuffer,
    [in] ULONG32 outBufferSize,
    [out, size_is(outBufferSize)] BYTE* outBuffer);
```

## <a name="parameters"></a>Parâmetros

`reqCode`\
no Tipo de solicitação a ser enviado.

`inBufferSize`\
[in] tamanho do buffer de entrada a ser passado.

`inBuffer`\
[in, size_is (InBufferSize)] Ponteiro de buffer para os dados brutos a serem enviados na solicitação.

`outBufferSize`\
no Tamanho do buffer de saída.

`outBuffer`\
[fora, size_is (OutBufferSize)] Ponteiro de buffer a ser usado para armazenar a resposta de solicitação.

## <a name="remarks"></a>Comentários

O método fornecido faz parte da `IXCLRDataModule` interface e corresponde ao slot 37th da tabela de métodos virtuais.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).
**Cabeçalho:** Nenhuma **biblioteca:** nenhuma **.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Interface IXCLRDataModule](ixclrdatamodule-interface.md)
