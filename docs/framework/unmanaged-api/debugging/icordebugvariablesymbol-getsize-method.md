---
description: 'Saiba mais sobre o método: ICorDebugVariableSymbol:: GetSize'
title: 'Método ICorDebugVariableSymbol:: GetSize'
ms.date: 03/30/2017
ms.assetid: add0cd9d-9a29-49b1-ae07-d9d3786b4ccd
ms.openlocfilehash: f4098bf5e053ab66dd7966d4b665cfad4dee01d5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790575"
---
# <a name="icordebugvariablesymbolgetsize-method"></a>Método ICorDebugVariableSymbol:: GetSize

Obtém o tamanho de uma variável em bytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSize(  
   [out] ULONG32 *pcbValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pcbValue`  
 Um ponteiro para um inteiro sem sinal de 32 bits contendo o tamanho da variável.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugVariableSymbol](icordebugvariablesymbol-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
