---
description: 'Saiba mais sobre o método: ICorDebugValue:: GetSize'
title: Método ICorDebugValue::GetSize
ms.date: 03/30/2017
api_name:
- ICorDebugValue.GetSize
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue::GetSize
helpviewer_keywords:
- GetSize method, ICorDebugValue interface [.NET Framework debugging]
- ICorDebugValue::GetSize method [.NET Framework debugging]
ms.assetid: 445a9ee3-e050-4f3a-931a-96b0efb00110
topic_type:
- apiref
ms.openlocfilehash: 3fc2582990d58fa2e42f240dfd3e563eed34e372
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690334"
---
# <a name="icordebugvaluegetsize-method"></a>Método ICorDebugValue::GetSize

Obtém o tamanho, em bytes, deste objeto "ICorDebugValue".  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSize (  
    [out] ULONG32   *pSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pSize`  
 fora O tamanho, em bytes, deste objeto de valor.  
  
## <a name="remarks"></a>Comentários  

 Se o tipo do valor for um tipo de referência, esse método retornará o tamanho do ponteiro em vez do tamanho do objeto.  
  
 O `ICorDebugValue::GetSize` método retorna `COR_E_OVERFLOW` para objetos com mais de 4 GB em plataformas de 64 bits. Use o método [ICorDebugValue3:: GetSize64](icordebugvalue3-getsize64-method.md) em vez de objetos com mais de 4 GB.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método GetSize64](icordebugvalue3-getsize64-method.md)
