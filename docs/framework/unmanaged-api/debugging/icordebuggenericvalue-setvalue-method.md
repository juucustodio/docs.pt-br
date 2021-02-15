---
description: 'Saiba mais sobre: método ICorDebugGenericValue:: SetValue'
title: Método ICorDebugGenericValue::SetValue
ms.date: 03/30/2017
api_name:
- ICorDebugGenericValue.SetValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGenericValue::SetValue
helpviewer_keywords:
- ICorDebugGenericValue::SetValue method [.NET Framework debugging]
- SetValue method, ICorDebugGenericValue interface [.NET Framework debugging]
ms.assetid: ed4c6458-0435-44fc-8e78-8ba00be362f2
topic_type:
- apiref
ms.openlocfilehash: e284d9987c8428fadedde0024fd3c65a0d8fe7a0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791472"
---
# <a name="icordebuggenericvaluesetvalue-method"></a>Método ICorDebugGenericValue::SetValue

Copia um novo valor do buffer especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetValue (  
    [in] void      *pFrom  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pFrom`  
 no Um ponteiro para o buffer do qual copiar o valor.  
  
## <a name="remarks"></a>Comentários  

 Para tipos de referência, o valor é a referência, não o conteúdo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
