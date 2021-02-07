---
description: 'Saiba mais sobre: método ICorDebugReferenceValue:: SetValue'
title: Método ICorDebugReferenceValue::SetValue
ms.date: 03/30/2017
api_name:
- ICorDebugReferenceValue.SetValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugReferenceValue::SetValue
helpviewer_keywords:
- SetValue method, ICorDebugReferenceValue interface [.NET Framework debugging]
- ICorDebugReferenceValue::SetValue method [.NET Framework debugging]
ms.assetid: 3d3f6eec-d772-401f-a028-1a2ecdc31e95
topic_type:
- apiref
ms.openlocfilehash: 44909962d2716ddb606d98a2f6b3804247c581cd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690906"
---
# <a name="icordebugreferencevaluesetvalue-method"></a>Método ICorDebugReferenceValue::SetValue

Define o endereço de memória especificado. Ou seja, esse método define esse ICorDebugReferenceValue para apontar para um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetValue (  
    [in] CORDB_ADDRESS    value  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `value`  
 no Um `CORDB_ADDRESS` valor que especifica o endereço do objeto para o qual este `ICorDebugReferenceValue` aponta.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
