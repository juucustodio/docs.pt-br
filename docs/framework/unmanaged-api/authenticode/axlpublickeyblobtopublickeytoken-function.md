---
description: 'Saiba mais sobre: _AxlPublicKeyBlobToPublicKeyToken função'
title: Função _AxlPublicKeyBlobToPublicKeyToken
ms.date: 03/30/2017
api_name:
- _AxlPublicKeyBlobToPublicKeyToken
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: 2d92a746-d68c-4f53-a16e-727f071a2d80
topic_type:
- apiref
ms.openlocfilehash: df0b484bad64051eb892d4898a6c90777cc2d5cf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781929"
---
# <a name="_axlpublickeyblobtopublickeytoken-function"></a>\_Função AxlPublicKeyBlobToPublicKeyToken

Computa o token de chave pública do nome forte de um formato CSP PUBLICKEYBLOB.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT _AxlPublicKeyBlobToPublicKeyToken (
    [in]  PCCERT_CHAIN_CONTEXT   pCspPublicKeyBlob,
    [out] LPWSTR                 *ppwszPublicKeyToken
);
```

## <a name="parameters"></a>Parâmetros

 `pCspPublicKeyBlob`\
 [in] O blob da chave pública CSP.

 `ppwszPublicKeyHash`\
 [out] Um ponteiro para WCHAR * para receber o hash da chave pública com codificação hexadecimal.

## <a name="return-value"></a>Valor retornado

 `S_OK` se a função for bem-sucedida; caso contrário, `S_FALSE`.

## <a name="requirements"></a>Requisitos

**Assembly**: clr.dll

## <a name="see-also"></a>Consulte também

- [Authenticode](index.md)
