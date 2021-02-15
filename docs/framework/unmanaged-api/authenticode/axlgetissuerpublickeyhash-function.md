---
description: 'Saiba mais sobre: _AxlGetIssuerPublicKeyHash função'
title: Função _AxlGetIssuerPublicKeyHash
ms.date: 03/30/2017
api_name:
- _AxlGetIssuerPublicKeyHash
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: fb626b41-b888-4625-84c3-2c02b5e3866f
topic_type:
- apiref
ms.openlocfilehash: 586a072b33376a2fdade119fe3db0f48addfa3f5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99747355"
---
# <a name="_axlgetissuerpublickeyhash-function"></a>\_Função AxlGetIssuerPublicKeyHash

Recupera o hash SHA-1 da chave pública associada à chave privada usada para assinar o certificado especificado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT _AxlGetIssuerPublicKeyHash (
    [in]  IN PCRYPT_DATA_BLOB   pChainContext,
    [out] LPWSTR                *ppwszPublicKeyHash
);
```

## <a name="parameters"></a>Parâmetros

 `pChainContext`\
 [in] O blob da chave pública CSP. Consulte a estrutura de [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob) .

 `ppwszPublicKeyHash`\
 [out] Um ponteiro para WCHAR * para receber o token de chave pública com codificação hexadecimal.

## <a name="return-value"></a>Valor retornado

 `S_OK` se a função for bem-sucedida; caso contrário, `S_FALSE`.

## <a name="requirements"></a>Requisitos

**Assembly**: clr.dll

## <a name="see-also"></a>Consulte também

- [Authenticode](index.md)
