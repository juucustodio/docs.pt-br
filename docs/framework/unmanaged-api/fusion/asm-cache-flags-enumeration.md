---
description: 'Saiba mais sobre: enumeração de ASM_CACHE_FLAGS'
title: Enumeração ASM_CACHE_FLAGS
ms.date: 03/30/2017
api_name:
- ASM_CACHE_FLAGS
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- ASM_CACHE_FLAGS
helpviewer_keywords:
- ASM_CACHE_FLAGS enumeration [.NET Framework fusion]
ms.assetid: 82e9a7da-321b-48b8-b239-52eaffda6be8
topic_type:
- apiref
ms.openlocfilehash: 866f61d2960074495ed036e3a8e89ebceec74e87
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761428"
---
# <a name="asm_cache_flags-enumeration"></a>Enumeração ASM_CACHE_FLAGS

Indica a origem de um assembly que é representado por [IAssemblyCacheItem](iassemblycacheitem-interface.md) no cache de assembly global.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    ASM_CACHE_ZAP       = 0x01,  
    ASM_CACHE_GAC       = 0x02,  
    ASM_CACHE_DOWNLOAD  = 0x04,  
    ASM_CACHE_ROOT      = 0x08,  
    ASM_CACHE_ROOT_EX   = 0x80  
} ASM_CACHE_FLAGS;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`ASM_CACHE_ZAP`|Enumera o cache de assemblies pré-compilados usando Ngen.exe.|  
|`ASM_CACHE_GAC`|Enumera o cache de assembly global.|  
|`ASM_CACHE_DOWNLOAD`|Enumera os assemblies que foram baixados sob demanda ou que foram copiados por sombra.|  
|`ASM_CACHE_ROOT`|Indica que a função [GetCachePath](getcachepath-function.md) deve retornar o caminho para o cache de assembly global para a versão 2,0 do Common Language Runtime (CLR). Significativo apenas no contexto de uma chamada para [GetCachePath](getcachepath-function.md).|  
|`ASM_CACHE_ROOT_EX`|Indica que a função [GetCachePath](getcachepath-function.md) deve retornar o caminho para o cache de assembly global para CLR versão 4. Significativo apenas no contexto de uma chamada para [GetCachePath](getcachepath-function.md).|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Função GetCachePath](getcachepath-function.md)
- [Interface IAssemblyCacheItem](iassemblycacheitem-interface.md)
- [Enumerações Fusion](fusion-enumerations.md)
