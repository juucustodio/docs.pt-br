---
description: 'Saiba mais sobre: método ICorDebugDebugEvent:: GetThread'
title: Método ICorDebugDebugEvent::GetThread
ms.date: 03/30/2017
ms.assetid: 4f2e9a2c-8369-4a07-a881-ad5422626353
ms.openlocfilehash: 1d476603572f31882f481d414e483c6712f1b5fc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710394"
---
# <a name="icordebugdebugeventgetthread-method"></a>Método ICorDebugDebugEvent::GetThread

Obtém o thread no qual o evento ocorreu.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetThread(  
        [out]ICorDebugThread **ppThread  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 ppThread  
 [out] Um ponteiro para o endereço de um objeto ICorDebugThread que representa o thread no qual o evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugDebugEvent](icordebugdebugevent-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
