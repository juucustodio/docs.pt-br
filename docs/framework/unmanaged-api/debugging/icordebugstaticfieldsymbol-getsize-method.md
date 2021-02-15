---
description: 'Saiba mais sobre o método: ICorDebugStaticFieldSymbol:: GetSize'
title: 'Método ICorDebugStaticFieldSymbol:: GetSize'
ms.date: 03/30/2017
ms.assetid: 72389860-7e37-4656-ba46-b6aeee1860f8
ms.openlocfilehash: f6fd2fe60d7cb8a77dcff5ca259d05ae1ef195ed
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794683"
---
# <a name="icordebugstaticfieldsymbolgetsize-method"></a>Método ICorDebugStaticFieldSymbol:: GetSize

Obtém o tamanho em bytes do campo estático.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSize(  
   [out] ULONG32 *pcbSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pcbSize`  
 fora Um ponteiro para o comprimento do campo.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugStaticFieldSymbol](icordebugstaticfieldsymbol-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
