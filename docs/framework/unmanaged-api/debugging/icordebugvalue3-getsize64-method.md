---
description: 'Saiba mais sobre o método: ICorDebugValue3:: GetSize64'
title: Método ICorDebugValue3::GetSize64
ms.date: 03/30/2017
api_name:
- ICorDebugValue3::GetSize64
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue3::GetSize64
helpviewer_keywords:
- GetSize64 method, ICorDebugValue3 interface [.NET Framework debugging]
- ICorDebugValue3::GetSize64 method [.NET Framework debugging]
ms.assetid: fee56a29-3154-4192-958d-71da2ced3740
topic_type:
- apiref
ms.openlocfilehash: ce7db5211c6a8fc16b58e0197fa3142b5b744d96
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690191"
---
# <a name="icordebugvalue3getsize64-method"></a>Método ICorDebugValue3::GetSize64

Obtém o tamanho, em bytes, deste objeto [ICorDebugValue3](icordebugvalue3-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSize64(  
    [out] ULONG64 *pSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 pSize  
 fora Um ponteiro para o tamanho, em bytes, deste objeto.  
  
## <a name="remarks"></a>Comentários  

 Se o tipo desse valor for um tipo de referência, esse método retornará o tamanho do ponteiro em vez do tamanho do objeto.  
  
 O `ICorDebugValue3::GetSize` método difere do método [ICorDebugValue:: GetSize](icordebugvalue-getsize-method.md) no tipo de seu parâmetro de saída. Em [ICorDebugValue:: GetSize](icordebugvalue-getsize-method.md), o parâmetro de saída é a `ULONG32` ; in `ICorDebugValue3::GetSize` , é um `ULONG64` . Isso permite que a interface [ICorDebugValue3](icordebugvalue3-interface.md) relate o tamanho das matrizes que excedem 2GB.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugValue3](icordebugvalue3-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
