---
description: 'Saiba mais sobre o método: ICorDebugObjectValue2:: GetVirtualMethodAndType'
title: Método ICorDebugObjectValue2::GetVirtualMethodAndType
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue2.GetVirtualMethodAndType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue2::GetVirtualMethodAndType
helpviewer_keywords:
- GetVirtualMethodAndType method [.NET Framework debugging]
- ICorDebugObjectValue2::GetVirtualMethodAndType method
ms.assetid: 621b4543-a8f7-4117-98e4-930992cd688a
topic_type:
- apiref
ms.openlocfilehash: 73866cc902d60316e3f1f31a86473116c0bff129
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781916"
---
# <a name="icordebugobjectvalue2getvirtualmethodandtype-method"></a>Método ICorDebugObjectValue2::GetVirtualMethodAndType

Este método ainda não foi implementado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetVirtualMethodAndType (  
    [in] mdMemberRef          memberRef,  
    [out] ICorDebugFunction   **ppFunction,  
    [out] ICorDebugType       **ppType  
);  
```  
  
## <a name="remarks"></a>Comentários  

 Obtém ponteiros de interface para as instâncias "ICorDebugFunction" e "ICorDebugType" que representam o método e tipo mais derivados para a referência de membro especificada.  
  
## <a name="see-also"></a>Confira também
