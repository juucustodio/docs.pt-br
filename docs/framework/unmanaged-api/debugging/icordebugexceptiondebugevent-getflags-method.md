---
description: 'Saiba mais sobre o método: ICorDebugExceptionDebugEvent:: GetFlags'
title: 'Método ICorDebugExceptionDebugEvent:: GetFlags'
ms.date: 03/30/2017
ms.assetid: 73225303-8852-487e-9a0e-9f0cb95e99d9
ms.openlocfilehash: 54a6c9b0dff2346ca130f80e72fe06dbb3017f10
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99693467"
---
# <a name="icordebugexceptiondebugeventgetflags-method"></a>Método ICorDebugExceptionDebugEvent:: GetFlags

Obtém um sinalizador que indica se a exceção pode ser interceptada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFlags(  
   [out] CorDebugExceptionFlags *pdwFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pdwFlags`  
 fora Um ponteiro para um valor [CorDebugExceptionFlags](cordebugexceptionflags-enumeration.md) que indica se a exceção pode ser interceptada.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugExceptionDebugEvent](icordebugexceptiondebugevent-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
