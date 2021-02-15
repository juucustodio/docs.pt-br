---
description: 'Saiba mais sobre: enumeração de COR_GC_STAT_TYPES'
title: Enumeração COR_GC_STAT_TYPES
ms.date: 03/30/2017
api_name:
- COR_GC_STAT_TYPES
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_STAT_TYPES
helpviewer_keywords:
- COR_GC_STAT_TYPES enumeration [.NET Framework hosting]
ms.assetid: fc51d6db-f7f8-408b-b93d-c166fc712c99
topic_type:
- apiref
ms.openlocfilehash: c4ea3175c777d49a5d6cffdf506f42e479784971
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799793"
---
# <a name="cor_gc_stat_types-enumeration"></a>Enumeração COR_GC_STAT_TYPES

Especifica as estatísticas a serem registradas para uma coleta de lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    COR_GC_COUNTS                 = 0x00000001  
    COR_GC_MEMORYUSAGE            = 0x00000002  
} COR_GC_STAT_TYPES;  
```  
  
## <a name="remarks"></a>Comentários  

 Essa enumeração Especifica quais estatísticas na estrutura de [COR_GC_STATS](cor-gc-stats-structure.md) devem ser definidas pelo método [ICLRGCManager:: GetStats](iclrgcmanager-getstats-method.md) .  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`COR_GC_COUNTS`|Registra o número de coletas de lixo executadas para cada geração.|  
|`COR_GC_MEMORYUSAGE`|Registra o uso de memória e estatísticas de tamanho da coleta de lixo.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** GCHost. idl, GCHost. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estrutura COR_GC_STATS](cor-gc-stats-structure.md)
- [Hospedando enumerações](hosting-enumerations.md)
