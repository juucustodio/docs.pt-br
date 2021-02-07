---
description: 'Saiba mais sobre: _AxlRSAKeyValueToPublicKeyToken função'
title: Função _AxlRSAKeyValueToPublicKeyToken
ms.date: 03/30/2017
api_name:
- _AxlRSAKeyValueToPublicKeyToken
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: d60f19fe-7bec-47ba-b60e-ba9ce66abf8c
topic_type:
- apiref
ms.openlocfilehash: 01fc4cdc1d9985375748307ca2d7fff97191c908
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99747264"
---
# <a name="_axlrsakeyvaluetopublickeytoken-function"></a>\_Função AxlRSAKeyValueToPublicKeyToken

Converte um Módulo e um Expoente em um token de chave pública com nome forte.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT _AxlRSAKeyValueToPublicKeyToken (
    [in]  PCRYPT_DATA_BLOB pModulusBlob,
    [in]  PCRYPT_DATA_BLOB pExponentBlob,
    [out] LPWSTR           *ppwszPublicKeyToken
);
```

## <a name="parameters"></a>Parâmetros

 `pModulusBlob`\
 no O blob de módulo codificado em Base64 (do \<Modulus> elemento).  Consulte a estrutura de [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob) .

 `pExponentBlob`\
 no O blob de expoente codificado em Base64 (do \<Exponent> elemento). Consulte a estrutura de [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob) .

 `ppwszPublicKeyToken`\
 [out] Um ponteiro para WCHAR * para receber o token de chave pública com codificação hexadecimal.

## <a name="return-value"></a>Valor retornado

 `S_OK` se a função for bem-sucedida. Caso contrário, retornará um código de erro.

## <a name="requirements"></a>Requisitos

**Assembly**: clr.dll

## <a name="see-also"></a>Consulte também

- [Authenticode](index.md)
