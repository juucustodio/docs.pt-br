---
description: 'Saiba mais sobre: ICorDebugHeapEnum:: Next Method'
title: Método ICorDebugHeapEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugHeapEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapEnum::Next
helpviewer_keywords:
- ICorDebugHeapEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugHeapEnum interface [.NET Framework debugging]
ms.assetid: 2221fd06-9e27-4113-972e-2530db8c3594
topic_type:
- apiref
ms.openlocfilehash: 22e81b9b0c4ac2027f932187b6f860d08adf6f97
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99691934"
---
# <a name="icordebugheapenumnext-method"></a>Método ICorDebugHeapEnum::Next

Obtém o número especificado de instâncias de [COR_HEAPOBJECT](cor-heapobject-structure.md) que contêm informações sobre objetos no heap gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next(  
    [in] ULONG celt,    [out, size_is(celt), length_is(*pceltFetched)] COR_HEAPOBJECT  objects[],
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 celt  
 no O número de objetos a serem recuperados.  
  
 objetos  
 fora Uma matriz de ponteiros, cada um dos quais aponta para um objeto [COR_HEAPOBJECT](cor-heapobject-structure.md) que fornece informações sobre um objeto no heap gerenciado.  
  
 pceltFetched  
 fora Um ponteiro para o número de objetos [COR_HEAPOBJECT](cor-heapobject-structure.md) realmente retornados em `objects` . Esse valor pode ser `null` se `celt` for 1.  
  
## <a name="remarks"></a>Comentários  

 O `COR_HEAPOBJECT.type` campo é o identificador de uma interface com contada com referência aninhada. Essa referência deve ser liberada pelo chamador de `ICorDebugHeapEnum::Next` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugHeapEnum](icordebugheapenum-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
