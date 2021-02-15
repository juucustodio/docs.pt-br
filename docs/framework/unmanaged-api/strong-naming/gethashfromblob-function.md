---
description: 'Saiba mais sobre: função GetHashFromBlob'
title: Função GetHashFromBlob
ms.date: 03/30/2017
api_name:
- GetHashFromBlob
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromBlob
helpviewer_keywords:
- GetHashFromBlob function [.NET Framework strong naming]
ms.assetid: b712d862-f2d0-4b55-87d4-65bbeadef982
topic_type:
- apiref
ms.openlocfilehash: dc5039e44440afa7a000bc61167faec0e5b6cc84
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736603"
---
# <a name="gethashfromblob-function"></a>Função GetHashFromBlob

Obtém um hash do assembly no endereço de memória especificado, usando o algoritmo de hash especificado.

Esta função foi preterida. Em vez disso, use o método [ICLRStrongName:: GetHashFromBlob](../hosting/iclrstrongname-gethashfromblob-method.md) .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetHashFromBlob (
    [in]  BYTE    *pbBlob,
    [in]  DWORD   cchBlob,
    [in, out] unsigned int   *piHashAlg,
    [out] BYTE    *pbHash,
    [in]  DWORD   cchHash,
    [out] DWORD   *pchHash
);
```

## <a name="parameters"></a>Parâmetros

`pbBlob`\
no Um ponteiro para o endereço do bloco de memória com hash.

`cchBlob`\
no O comprimento, em bytes, do bloco de memória.

`piHashAlg`\
[entrada, saída] Uma constante que especifica o algoritmo de hash. Use zero para o algoritmo padrão.

`pbHash`\
fora O buffer de hash retornado.

`cchHash`\
no O tamanho máximo solicitado de `pbHash` .

`pchHash`\
fora O tamanho, em bytes, do retornado `pbHash` .

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** StrongName. h

**Biblioteca:** Incluído como um recurso no MsCorEE.dll

**.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Método GetHashFromBlob](../hosting/iclrstrongname-gethashfromblob-method.md)
- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
