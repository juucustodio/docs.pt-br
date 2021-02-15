---
description: 'Saiba mais sobre: função CertTimestampAuthenticodeLicense'
title: Função CertTimestampAuthenticodeLicense
ms.date: 03/30/2017
api_name:
- CertTimestampAuthenticodeLicense
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: d468325a-21c5-43ce-8567-84e342b22308
topic_type:
- apiref
ms.openlocfilehash: 79b1a924a99a76c18e6434abfed0a90da71eb6f9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772910"
---
# <a name="certtimestampauthenticodelicense-function"></a>Função CertTimestampAuthenticodeLicense

Carimbo de data/hora em uma licença Authenticode XrML.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CertTimestampAuthenticodeLicense (
    [in]  PCRYPT_DATA_BLOB   pSignedLicenseBlob,
    [in]  LPCWSTR            pwszTimestampURI,
    [out] PCRYPT_DATA_BLOB   pTimestampSignatureBlob
);
```

## <a name="parameters"></a>Parâmetros

 `pSignedLicenseBlob`\
 [in] A licença Authenticode XrML assinada a receber o carimbo de data/hora. Consulte a estrutura de [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob) .

 `pwszTimestampURI`\
 [in] O URI do servidor de carimbo de data/hora.

 `pTimestampSignatureBlob`\
 [out] Um ponteiro para CRYPT_DATA_BLOB para receber a assinatura do carimbo de data/hora codificado por base64. É responsabilidade do chamador gratuita `pTimestampSignatureBlob` -> `pbData` com `HepFree()` após o uso. Consulte a estrutura de [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob) .

## <a name="remarks"></a>Comentários

 A assinatura do carimbo de data/hora é, na realidade, uma mensagem PKCS #7 SignedData cujo conteúdo é o formulário binário do SignatureValue da assinatura da licença. Basicamente, isso funciona como uma referenda da licença.

## <a name="return-value"></a>Valor retornado

 `S_OK` se a função for bem-sucedida. Caso contrário, retornará um código de erro.

## <a name="requirements"></a>Requisitos

**Assembly**: clr.dll

## <a name="see-also"></a>Consulte também

- [Authenticode](index.md)
