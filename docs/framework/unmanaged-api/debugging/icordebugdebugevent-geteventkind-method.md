---
description: 'Saiba mais sobre o método: ICorDebugDebugEvent:: GetEventKind'
title: Método ICorDebugDebugEvent::GetEventKind
ms.date: 03/30/2017
ms.assetid: c37aaceb-c948-46bd-a943-08be4cbb76f4
ms.openlocfilehash: 9e15eb82195fae8aa3797ea47cb04d0bb407d2ad
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764314"
---
# <a name="icordebugdebugeventgeteventkind-method"></a>Método ICorDebugDebugEvent::GetEventKind

Indica o tipo de evento que este objeto `ICorDebugDebugEvent` representa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetEventKind(  
    [out]CorDebugDebugEventKind *pDebugEventKind  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 pDebugEventKind  
 Um ponteiro para um membro de enumeração [CorDebugDebugEventKind](cordebugdebugeventkind-enumeration.md) que indica o tipo de evento.  
  
## <a name="remarks"></a>Comentários  

 Com base no valor de `pDebugEventKind`, você pode chamar `QueryInterface` para obter uma interface de evento de depuração mais precisa com dados adicionais.  
  
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
