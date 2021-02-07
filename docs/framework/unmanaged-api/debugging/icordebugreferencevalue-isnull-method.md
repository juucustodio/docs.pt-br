---
description: 'Saiba mais sobre: método ICorDebugReferenceValue:: IsNull'
title: Método ICorDebugReferenceValue::IsNull
ms.date: 03/30/2017
api_name:
- ICorDebugReferenceValue.IsNull
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugReferenceValue::IsNull
helpviewer_keywords:
- IsNull method, ICorDebugReferenceValue interface [.NET Framework debugging]
- ICorDebugReferenceValue::IsNull method [.NET Framework debugging]
ms.assetid: 99e8c8d7-a1c0-47c8-9dbd-03e0b2bcb4d5
topic_type:
- apiref
ms.openlocfilehash: 9fffc869e20d1d3aa3a347ff2e026e6b55e6bd4f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99691010"
---
# <a name="icordebugreferencevalueisnull-method"></a>Método ICorDebugReferenceValue::IsNull

Obtém um valor que indica se este ICorDebugReferenceValue é um valor nulo; nesse caso, o `ICorDebugReferenceValue` não aponta para um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsNull (  
    [out] BOOL   *pbNull  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbNull`  
 fora Um ponteiro para um valor booliano que é `true` se esse `ICorDebugReferenceValue` objeto for nulo; caso contrário, `pbNull` será `false` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
