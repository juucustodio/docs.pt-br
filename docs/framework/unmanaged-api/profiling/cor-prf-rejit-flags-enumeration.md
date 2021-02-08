---
description: 'Saiba mais sobre: enumeração de COR_PRF_REJIT_FLAGS'
title: Enumeração COR_PRF_REJIT_FLAGS
ms.date: 08/06/2019
api_name:
- COR_PRF_REJIT_FLAGS Enumeration
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_REJIT_FLAGS
helpviewer_keywords:
- COR_PRF_REJIT_FLAGS enumeration [.NET Framework profiling]
topic_type:
- apiref
author: davmason
ms.author: davmason
ms.openlocfilehash: a27b6d90b51254560f25fbadb18ac95fe838ab2b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789015"
---
# <a name="cor_prf_rejit_flags-enumeration"></a>Enumeração COR_PRF_REJIT_FLAGS

Contém valores que indicam como a API [ICorProfilerInfo10:: RequestReJITWithInliners](icorprofilerinfo10-requestrejitwithinliners-method.md) deve se comportar.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum  
{
    COR_PRF_REJIT_BLOCK_INLINING = 0x1,
    COR_PRF_REJIT_INLINING_CALLBACKS    = 0x2
} COR_PRF_REJIT_FLAGS;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`COR_PRF_REJIT_BLOCK_INLINING`| Os métodos ReJITted serão impedidos de serem embutidos em outros métodos. |  
|`COR_PRF_REJIT_INLINING_CALLBACKS`| Receber `GetFunctionParameters` retornos de chamada para todos os métodos que embutiram os métodos solicitados a serem ReJITteddos. |  

## <a name="requirements"></a>Requisitos  

 **Plataformas:** Consulte [sistemas operacionais com suporte do .NET Core](../../../core/install/windows.md?pivots=os-windows).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_core_22](../../../../includes/net-core-22-md.md)]
  
## <a name="see-also"></a>Consulte também

- [Criando perfil de enumerações](profiling-enumerations.md)
