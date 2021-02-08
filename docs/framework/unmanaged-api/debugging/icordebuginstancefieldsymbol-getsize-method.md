---
description: 'Saiba mais sobre o método: ICorDebugInstanceFieldSymbol:: GetSize'
title: 'Método ICorDebugInstanceFieldSymbol:: GetSize'
ms.date: 03/30/2017
ms.assetid: a4af1e3b-6a9f-4855-95ba-5317565c8e2b
ms.openlocfilehash: fa143620b57ec053ab26ff79b7ea2b2f386431e7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791147"
---
# <a name="icordebuginstancefieldsymbolgetsize-method"></a>Método ICorDebugInstanceFieldSymbol:: GetSize

Obtém o tamanho em bytes do campo de instância.  
  
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

- [Interface ICorDebugInstanceFieldSymbol](icordebuginstancefieldsymbol-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
