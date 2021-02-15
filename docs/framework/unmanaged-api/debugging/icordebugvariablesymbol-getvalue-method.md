---
description: 'Saiba mais sobre: método ICorDebugVariableSymbol:: GetValue'
title: 'Método ICorDebugVariableSymbol:: GetValue'
ms.date: 03/30/2017
ms.assetid: 90abece1-392e-4ade-94a1-30c75b0f7074
ms.openlocfilehash: ccd7eae5cc4740e83d0210a903ba0e7778aa8896
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790562"
---
# <a name="icordebugvariablesymbolgetvalue-method"></a>Método ICorDebugVariableSymbol:: GetValue

Obtém o valor de uma variável como uma matriz de bytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetValue(  
   [in] ULONG32 offset,  
   [in] ULONG32 cbContext,  
   [in, size_is(cbContext)] BYTE context[],  
   [in] ULONG32 cbValue,  
   [out] ULONG32 *pcbValue,  
   [out, size_is(cbValue), length_is(*pcbValue)] BYTE pValue[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `offset`  
 no O deslocamento inicial na variável a partir da qual o valor deve ser lido. Esse parâmetro é usado ao ler campos de membro em um objeto.  
  
 `cbContext`  
 no O tamanho em bytes do `context` argumento.  
  
 `context`  
 no O contexto de thread usado para ler o valor.  
  
 `cbValue`  
 no O tamanho em bytes do `pValue` buffer.  
  
 `pcbValue`  
 fora O número de bytes realmente gravados no `pValue` buffer.  
  
 `pValue`  
 fora Uma matriz de bytes que contém o valor da variável.  
  
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
