---
description: 'Saiba mais sobre: ICorDebugHeapSegmentEnum:: Next Method'
title: Método ICorDebugHeapSegmentEnum::Next
ms.date: 03/30/2017
api_name:
- Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapSegmentEnum::Next
helpviewer_keywords:
- ICorDebugHeapSegmentEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugHeapSegmentEnum interface [.NET Framework debugging]
ms.assetid: 51625fd0-7399-49c7-b22b-5dfb05451fe6
topic_type:
- apiref
ms.openlocfilehash: 8d2ddfb4df82969fa9cf580ed8a7f903f9d6c260
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803669"
---
# <a name="icordebugheapsegmentenumnext-method"></a>Método ICorDebugHeapSegmentEnum::Next

Obtém o número especificado de instâncias de [COR_SEGMENT](cor-segment-structure.md) que contêm informações sobre regiões de memória do heap gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next(  
    [in] ULONG celt,    [out, size_is(celt), length_is(*pceltFetched)] COR_SEGMENT segments[],
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 celt  
 no O número de segmentos a serem recuperados.  
  
 segmentos  
 fora Uma matriz de ponteiros, cada um dos quais aponta para um objeto [COR_SEGMENT](cor-segment-structure.md) que fornece informações sobre uma região de memória no heap gerenciado.  
  
 pceltFetched  
 fora Um ponteiro para o número de objetos [COR_SEGMENT](cor-segment-structure.md) realmente retornados em `segments` . Esse valor pode ser `null` se `celt` for 1.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
