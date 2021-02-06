---
description: 'Saiba mais sobre o método: ICorDebugProcess5:: EnumerateHeapRegions'
title: Método ICorDebugProcess5::EnumerateHeapRegions
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHeapRegions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHeapRegions
helpviewer_keywords:
- EnumerateHeapRegions method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeapRegions method [.NET Framework debugging]
ms.assetid: b1edba68-9c36-4f69-be9f-678ce0b33480
topic_type:
- apiref
ms.openlocfilehash: 034b1ebcd003e6854fa4f308b0464aac0a8c4839
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649839"
---
# <a name="icordebugprocess5enumerateheapregions-method"></a>Método ICorDebugProcess5::EnumerateHeapRegions

Obtém um enumerador para os intervalos de memória do heap gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateHeapRegions(  
   [out] ICorDebugHeapSegmentEnum **ppRegions  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppRegions`  
 fora Um ponteiro para o endereço de um objeto de interface [ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md) que é um enumerador para os intervalos de memória em que os objetos residem no heap gerenciado.  
  
## <a name="remarks"></a>Comentários  

 Antes de chamar o `ICorDebugProcess5::EnumerateHeapRegions` método, você deve chamar o método [ICorDebugProcess5:: GetGCHeapInformation](icordebugprocess5-getgcheapinformation-method.md) e examinar o valor do `areGCStructuresValid` campo do objeto de [COR_HEAPINFO](cor-heapinfo-structure.md) retornado para garantir que o heap de coleta de lixo em seu estado atual seja enumerável. Além disso, o `ICorDebugProcess5::EnumerateHeapRegions` método retorna `E_FAIL` se você anexar muito cedo no tempo de vida do processo, antes que as regiões de memória sejam criadas.  
  
 Esse método é garantido para enumerar todas as regiões de memória que podem conter objetos gerenciados, mas não garante que os objetos gerenciados realmente residam nessas regiões. O objeto da coleção [ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md) pode incluir regiões de memória vazias ou reservadas.  
  
 O objeto de interface [ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md) é um enumerador padrão derivado da interface ICorDebugEnum que permite que você enumere [COR_SEGMENT](cor-segment-structure.md) objetos. Cada objeto de [COR_SEGMENT](cor-segment-structure.md) fornece informações sobre o intervalo de memória de um segmento específico, juntamente com a geração dos objetos nesse segmento.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugProcess5](icordebugprocess5-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
