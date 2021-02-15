---
description: 'Saiba mais sobre o método: IXCLRDataProcess:: GetAppDomainByUniqueId'
title: 'Método IXCLRDataProcess:: GetAppDomainByUniqueId'
ms.date: 01/16/2019
api.name:
- IXCLRDataProcess::GetAppDomainByUniqueId Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataProcess::GetAppDomainByUniqueId Method
helpviewer.keywords:
- IXCLRDataProcess::GetAppDomainByUniqueId Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 7087362efbb810fcb6e1b6f7eb9f23c54c38fade
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800663"
---
# <a name="ixclrdataprocessgetappdomainbyuniqueid-method"></a>Método IXCLRDataProcess:: GetAppDomainByUniqueId

Obtém um `AppDomain` em um processo com base em seu identificador exclusivo.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetAppDomainByUniqueID(
    [in] ULONG64               id,
    [out] IXCLRDataAppDomain **appDomain
);
```

## <a name="parameters"></a>Parâmetros

`id`\
no O identificador exclusivo do AppDomain

`appDomain`\
fora O AppDomain

## <a name="remarks"></a>Comentários

O método fornecido faz parte da `IXCLRDataProcess` interface e corresponde ao slot 20 da tabela de métodos virtuais. O `IXCLRDataAppDomain*` retornado é usado para interação com outras APIs.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).
**Cabeçalho:** Nenhuma **biblioteca:** nenhuma **.NET Framework versões:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [Interface IXCLRDataProcess](ixclrdataprocess-interface.md)
