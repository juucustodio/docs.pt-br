---
description: 'Saiba mais sobre: função CertFreeAuthenticodeSignerInfo'
title: Função CertFreeAuthenticodeSignerInfo
ms.date: 03/30/2017
api_name:
- CertFreeAuthenticodeSignerInfo
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: 8029633c-b6e4-4665-a7c2-89607c3247ef
topic_type:
- apiref
ms.openlocfilehash: 6e8a97e8fee37d885c7d32102ed8cc7654992223
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772972"
---
# <a name="certfreeauthenticodesignerinfo-function"></a>Função CertFreeAuthenticodeSignerInfo

Libera recursos alocados para a estrutura de [AXL_AUTHENTICODE_SIGNER_INFO](axl-authenticode-signer-info-structure.md) .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CertFreeAuthenticodeSignerInfo (
    [in, out]  PAXL_AUTHENTICODE_SIGNER_INFO   pSignerInfo);
```

## <a name="parameters"></a>Parâmetros

 `pSignerInfo`\
 [in, out] Informações de signatário a serem liberadas. Consulte a estrutura de [AXL_AUTHENTICODE_SIGNER_INFO](axl-authenticode-signer-info-structure.md) .

## <a name="return-value"></a>Valor retornado

 `S_OK` se a função for bem-sucedida. Caso contrário, retornará um código de erro.

## <a name="requirements"></a>Requisitos

**Assembly**: clr.dll

## <a name="see-also"></a>Consulte também

- [Authenticode](index.md)
