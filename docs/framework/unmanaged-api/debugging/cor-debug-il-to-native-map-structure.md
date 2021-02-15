---
description: 'Saiba mais sobre: estrutura de COR_DEBUG_IL_TO_NATIVE_MAP'
title: Estrutura COR_DEBUG_IL_TO_NATIVE_MAP
ms.date: 03/30/2017
api_name:
- COR_DEBUG_IL_TO_NATIVE_MAP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_DEBUG_IL_TO_NATIVE_MAP
helpviewer_keywords:
- COR_DEBUG_IL_TO_NATIVE_MAP structure [.NET Framework debugging]
ms.assetid: 06f3b504-085f-4142-934a-25381fe23d4c
topic_type:
- apiref
ms.openlocfilehash: ec722b86f95e75d4ac00e04e8a602c6b6da64de5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99747186"
---
# <a name="cor_debug_il_to_native_map-structure"></a>Estrutura COR_DEBUG_IL_TO_NATIVE_MAP

Contém os deslocamentos que são usados ​​para mapear o código da MSIL (Microsoft intermediate language) para o código nativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct COR_DEBUG_IL_TO_NATIVE_MAP {  
    ULONG32  ilOffset;  
    ULONG32  nativeStartOffset;  
    ULONG32  nativeEndOffset;  
} COR_DEBUG_IL_TO_NATIVE_MAP;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`ilOffset`|O deslocamento do código MSIL.|  
|`nativeStartOffset`|O deslocamento do início do código nativo.|  
|`nativeEndOffset`|O deslocamento do final do código nativo.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorDebug. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método GetILToNativeMapping](../profiling/icorprofilerinfo-getiltonativemapping-method.md)
- [Método GetILToNativeMapping](icordebugcode-getiltonativemapping-method.md)
- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
