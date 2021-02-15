---
description: 'Saiba mais sobre: estrutura de COR_SEGMENT'
title: Estrutura COR_SEGMENT
ms.date: 03/30/2017
api_name:
- COR_SEGMENT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_SEGMENT
helpviewer_keywords:
- COR_SEGMENT structure [.NET Framework debugging]
ms.assetid: 93aeecb9-7fef-4545-8daf-f566dfc47084
topic_type:
- apiref
ms.openlocfilehash: 9bbc452b2c2036d019175ac1be8b9917ffa07b6a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712175"
---
# <a name="cor_segment-structure"></a>Estrutura COR_SEGMENT

Contém informações sobre uma região da memória no heap gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _COR_SEGMENT {  
    CORDB_ADDRESS start;
    CORDB_ADDRESS end;
    CorDebugGenerationTypes gen;
    ULONG heap;
} COR_SEGMENT;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`start`|O endereço inicial da região de memória.|  
|`end`|O endereço final da região de memória.|  
|`gen`|Um membro de enumeração [CorDebugGenerationTypes](cordebuggenerationtypes-enumeration.md) que indica a geração da região de memória.|  
|`heap`|O número de heap no qual reside a região de memória. Consulte a seção Comentários para obter mais informações.|  
  
## <a name="remarks"></a>Comentários  

 A estrutura `COR_SEGMENTS` representa uma região da memória no heap gerenciado.  Objetos `COR_SEGMENTS` são membros do objeto da coleção [ICorDebugHeapRegionEnum](icordebugheapsegmentenum-interface.md), que é preenchido chamando o método [ICorDebugProcess5::EnumerateHeapRegions](icordebugprocess5-enumerateheapregions-method.md).  
  
 O campo `heap` é o número de processadores, que corresponde ao heap que está sendo relatado. Para os coletores de lixo de estação de trabalho, seu valor é sempre zero, uma vez que estações de trabalho têm apenas um heap de coleta de lixo. Para os coletores de lixo do servidor, seu valor corresponde ao processador ao qual o heap está anexado. Observe que pode haver mais ou menos heaps de coleta de lixo que o número real de processadores devido a detalhes de implementação do coletor de lixo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
