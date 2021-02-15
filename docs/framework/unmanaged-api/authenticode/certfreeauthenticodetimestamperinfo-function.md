---
description: 'Saiba mais sobre: função CertFreeAuthenticodeTimestamperInfo'
title: Função CertFreeAuthenticodeTimestamperInfo
ms.date: 03/30/2017
api_name:
- CertFreeAuthenticodeTimestamperInfo
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: 3eb14c49-68c2-4516-ac89-e5bd7473831c
topic_type:
- apiref
ms.openlocfilehash: 5234a90ea1d0272a7409b1b0b4def2160b77a513
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772933"
---
# <a name="certfreeauthenticodetimestamperinfo-function"></a>Função CertFreeAuthenticodeTimestamperInfo

Libera recursos alocados para a estrutura de [AXL_AUTHENTICODE_TIMESTAMPER_INFO](axl-authenticode-timestamper-info-structure.md) .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CertFreeAuthenticodeTimestamperInfo (
    [in, out]  PAXL_AUTHENTICODE_TIMESTAMPER_INFO   pTimestamperInfo
);
```

## <a name="parameters"></a>Parâmetros

 `pTimestamperInfo`\
 [in, out] As informações do carimbo de data/hora que será liberado. Consulte a estrutura de [AXL_AUTHENTICODE_TIMESTAMPER_INFO](axl-authenticode-timestamper-info-structure.md) .

## <a name="return-value"></a>Valor retornado

 `S_OK` se a função for bem-sucedida. Caso contrário, retornará um código de erro.

## <a name="requirements"></a>Requisitos

**Assembly**: clr.dll

## <a name="see-also"></a>Consulte também

- [Authenticode](index.md)
