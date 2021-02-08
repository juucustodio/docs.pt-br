---
description: 'Saiba mais sobre o método: ICorDebugVariableSymbol:: GetName'
title: 'Método ICorDebugVariableSymbol:: GetName'
ms.date: 03/30/2017
ms.assetid: c922b7d4-44e5-45e4-aef3-cc9c35a0be80
ms.openlocfilehash: 4a3ba1dfebd256dcbb8374634a52f1feca5d9611
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790588"
---
# <a name="icordebugvariablesymbolgetname-method"></a>Método ICorDebugVariableSymbol:: GetName

Obtém o nome de uma variável.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetName(  
   [in] ULONG32 cchName,
   [out] ULONG32 *pcchName,
   [out, size_is(cchName), length_is(*pcchName)] WCHAR szName[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cchName`  
 no O número de caracteres no `szName` buffer.  
  
 `pcchName`  
 fora Um ponteiro para o número de caracteres realmente gravados no `szName` buffer.  
  
 `szName`  
 Um ponteiro para uma matriz de caracteres que contém o nome da variável.  
  
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
