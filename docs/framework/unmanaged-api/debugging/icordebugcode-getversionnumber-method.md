---
description: 'Saiba mais sobre: ICorDebugCode:: método GetVersionNumber'
title: Método ICorDebugCode::GetVersionNumber
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetVersionNumber
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetVersionNumber
helpviewer_keywords:
- GetVersionNumber method, ICorDebugCode interface [.NET Framework debugging]
- ICorDebugCode::GetVersionNumber method [.NET Framework debugging]
ms.assetid: c8e02518-679f-4e9f-8a28-ba4a89a3876f
topic_type:
- apiref
ms.openlocfilehash: 901342333bea3d455407602dde78bdccd0140d77
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764899"
---
# <a name="icordebugcodegetversionnumber-method"></a>Método ICorDebugCode::GetVersionNumber

Obtém o número baseado em um que identifica a versão do código que esse "ICorDebugCode" representa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetVersionNumber (
    [out] ULONG32    *nVersion
);
```

## <a name="parameters"></a>Parâmetros

 `nVersion`  
 fora Um ponteiro para o número de versão do código.

## <a name="remarks"></a>Comentários

 O número de versão é incrementado cada vez que uma operação de "Editar e continuar" (EnC) é executada no código.

## <a name="requirements"></a>Requisitos

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
