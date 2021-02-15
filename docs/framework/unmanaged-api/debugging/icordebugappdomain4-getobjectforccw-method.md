---
description: 'Saiba mais sobre o método: ICorDebugAppDomain4:: GetObjectForCCW'
title: Método ICorDebugAppDomain4::GetObjectForCCW
ms.date: 03/30/2017
ms.assetid: 2cacdb85-e7b8-42e7-b310-c3e8c22e5d33
ms.openlocfilehash: 5ba4923c933d02f5d6ad5c1fd8c4d0e2ddb410d3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754128"
---
# <a name="icordebugappdomain4getobjectforccw-method"></a>Método ICorDebugAppDomain4::GetObjectForCCW

Obtém um objeto gerenciado de um ponteiro de COM Callable Wrapper (CCW).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetObjectForCCW(  
   [in]CORDB_ADDRESS ccwPointer,
   [out]ICorDebugValue **ppManagedObject  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ccwPointer`  
 no Um ponteiro de COM Callable Wrapper (CCW).  
  
 `ppManagedObject`  
 fora Um ponteiro para o endereço de um objeto "ICorDebugValue" que representa o objeto gerenciado que corresponde ao ponteiro do CCW fornecido.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugAppDomain4](icordebugappdomain4-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
