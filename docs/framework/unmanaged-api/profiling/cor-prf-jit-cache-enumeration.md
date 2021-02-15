---
description: 'Saiba mais sobre: enumeração de COR_PRF_JIT_CACHE'
title: Enumeração COR_PRF_JIT_CACHE
ms.date: 03/30/2017
api_name:
- COR_PRF_JIT_CACHE
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_JIT_CACHE
helpviewer_keywords:
- COR_PRF_JIT_CACHE enumeration [.NET Framework profiling]
ms.assetid: e7b8f6b4-95bc-4ba5-b9eb-f5590a7326a4
topic_type:
- apiref
ms.openlocfilehash: 94b04b42504760be826f78cee0da3066f1936f32
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99648747"
---
# <a name="cor_prf_jit_cache-enumeration"></a>Enumeração COR_PRF_JIT_CACHE

Indica o resultado de uma busca de função armazenada em cache.  
  
> [!NOTE]
> `COR_PRF_CACHED_FUNCTION_FOUND` tem um valor de zero, portanto `COR_PRF_JIT_CACHE` não pode ser usado como um substituto booliano.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    COR_PRF_CACHED_FUNCTION_FOUND,  
    COR_PRF_CACHED_FUNCTION_NOT_FOUND  
} COR_PRF_JIT_CACHE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`COR_PRF_FUNCTION_FOUND`|A pesquisa encontrou a função.|  
|`COR_PRF_FUNCTION_NOT_FOUND`|A pesquisa não encontrou a função.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criando perfil de enumerações](profiling-enumerations.md)
