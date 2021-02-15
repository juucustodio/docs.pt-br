---
description: 'Saiba mais sobre o método: ICorDebugArrayValue:: GetBaseIndicies'
title: Método ICorDebugArrayValue::GetBaseIndicies
ms.date: 03/30/2017
api_name:
- ICorDebugArrayValue.GetBaseIndicies
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugArrayValue::GetBaseIndicies
helpviewer_keywords:
- ICorDebugArrayValue::GetBaseIndicies method [.NET Framework debugging]
- GetBaseIndicies method [.NET Framework debugging]
ms.assetid: 868b339b-acdb-4fe0-91c7-b85f4fba99eb
topic_type:
- apiref
ms.openlocfilehash: ac38123860cc3187b7dc2398b32244387d19c5ac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723110"
---
# <a name="icordebugarrayvaluegetbaseindicies-method"></a>Método ICorDebugArrayValue::GetBaseIndicies

Obtém o índice base de cada dimensão na matriz.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetBaseIndicies (  
    [in] ULONG32          cdim,  
    [out, size_is(cdim), length_is(cdim)]
        ULONG32           indicies[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cdim`  
 no O número de dimensões deste `ICorDebugArrayValue` objeto. Esse valor também é o tamanho da `indicies` matriz porque seu tamanho é igual ao número de dimensões do `ICorDebugArrayValue` objeto.  
  
 `indicies`  
 fora Uma matriz de inteiros, cada um dos quais é o índice base (ou seja, o índice inicial) de uma dimensão desse `ICorDebugArrayValue` objeto.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
