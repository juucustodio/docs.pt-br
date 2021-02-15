---
description: 'Saiba mais sobre: método ICorDebugValue:: GetType'
title: Método ICorDebugValue::GetType
ms.date: 03/30/2017
api_name:
- ICorDebugValue.GetType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue::GetType
helpviewer_keywords:
- ICorDebugValue::GetType method [.NET Framework debugging]
- GetType method, ICorDebugValue interface [.NET Framework debugging]
ms.assetid: 41e2d503-e1f1-407b-abe0-6a29adb3e0d1
topic_type:
- apiref
ms.openlocfilehash: 750e73634683a03e811d2756cc62c16b6dcea3de
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690318"
---
# <a name="icordebugvaluegettype-method"></a>Método ICorDebugValue::GetType

Obtém o tipo primitivo desse objeto "ICorDebugValue".  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetType (  
    [out] CorElementType   *pType  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pType`  
 fora Um ponteiro para um valor da enumeração "CorElementType" que indica o tipo do valor.  
  
## <a name="remarks"></a>Comentários  

 Se o objeto for um tipo de tempo de execução complexo, esse tipo poderá ser examinado por meio das subclasses apropriadas da `ICorDebugValue` interface. Por exemplo, "ICorDebugObjectValue", que herda de `ICorDebugValue` , representa um tipo complexo.  
  
 Os `GetType` métodos e [ICorDebugObjectValue:: GetClass](icordebugobjectvalue-getclass-method.md) retornam informações sobre o tipo de um valor. Eles são ambos substituídos pelo método [ICorDebugValue2:: Getexatotype](icordebugvalue2-getexacttype-method.md) com reconhecimento de genéricos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Confira também
