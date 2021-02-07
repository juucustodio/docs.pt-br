---
description: 'Saiba mais sobre o método: ICorDebugMemoryBuffer:: GetSize'
title: 'Método ICorDebugMemoryBuffer:: GetSize'
ms.date: 03/30/2017
ms.assetid: 9ffd5482-268e-4680-9fd1-bfb0b7d66450
ms.openlocfilehash: 7de23dd13a1e0ef841145e3845d7d0052ce3ef9a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754034"
---
# <a name="icordebugmemorybuffergetsize-method"></a>Método ICorDebugMemoryBuffer:: GetSize

Obtém o tamanho do buffer de memória em bytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSize(  
   [out] ULONG32 *pcbBufferLength  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pcbBufferLength`  
 fora Um ponteiro para o tamanho do buffer de memória.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugMemoryBuffer](icordebugmemorybuffer-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
