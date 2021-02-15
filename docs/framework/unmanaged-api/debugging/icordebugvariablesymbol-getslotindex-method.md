---
description: 'Saiba mais sobre o método: ICorDebugVariableSymbol:: GetSlotIndex'
title: 'Método ICorDebugVariableSymbol:: GetSlotIndex'
ms.date: 03/30/2017
ms.assetid: 09c19f5f-afc4-4e0c-bffe-cd7147bc7a43
ms.openlocfilehash: 3b5cba06a5e80ffa323d2e6521e9ec4666f6f5f3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790549"
---
# <a name="icordebugvariablesymbolgetslotindex-method"></a>Método ICorDebugVariableSymbol:: GetSlotIndex

Obtém o índice de slot gerenciado de uma variável local.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSlotIndex(  
   [out] ULONG32 *pSlotIndex  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pSlotIndex`  
 fora Um ponteiro para o índice de slot da variável local.  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` se bem-sucedido. `E_FAIL` se a variável for um argumento de função.  
  
## <a name="remarks"></a>Comentários  

 O índice de slot gerenciado de uma variável local pode ser usado para recuperar as informações de metadados da variável  
  
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
