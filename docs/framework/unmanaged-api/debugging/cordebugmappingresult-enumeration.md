---
description: 'Saiba mais sobre: Enumeração CorDebugMappingResult'
title: Enumeração CorDebugMappingResult
ms.date: 03/30/2017
api_name:
- CorDebugMappingResult
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugMappingResult
helpviewer_keywords:
- CorDebugMappingResult enumeration [.NET Framework debugging]
ms.assetid: 701281dd-2936-45c8-a1f0-3bf7332b093b
topic_type:
- apiref
ms.openlocfilehash: 03454e2fbfa8fabca89805ea51a6cfba27aa792f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801586"
---
# <a name="cordebugmappingresult-enumeration"></a>Enumeração CorDebugMappingResult

Fornece os detalhes sobre como o valor do ponteiro de instrução (IP) foi obtido.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugMappingResult {  
    MAPPING_PROLOG              = 0x1,  
    MAPPING_EPILOG              = 0x2,  
    MAPPING_NO_INFO             = 0x4,  
    MAPPING_UNMAPPED_ADDRESS    = 0x8,  
    MAPPING_EXACT               = 0x10,  
    MAPPING_APPROXIMATE         = 0x20,  
} CorDebugMappingResult;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`MAPPING_PROLOG`|O código nativo está no prólogo, portanto, o valor do IP é 0.|  
|`MAPPING_EPILOG`|O código nativo está em um epílogo, portanto, o valor do IP é o endereço da última instrução do método.|  
|`MAPPING_NO_INFO`|Nenhuma informação de mapeamento está disponível para o método, portanto, o valor do IP é 0.|  
|`MAPPING_UNMAPPED_ADDRESS`|Embora haja informações de mapeamento para o método, o endereço atual não pode ser mapeado para o código MSIL (Microsoft Intermediate Language). O valor do IP é 0.|  
|`MAPPING_EXACT`|O método é mapeado exatamente para o código MSIL ou o quadro foi interpretado, portanto, o valor do IP é preciso.|  
|`MAPPING_APPROXIMATE`|O método foi mapeado com êxito, mas o valor do IP pode ser aproximado.|  
  
## <a name="remarks"></a>Comentários  

 Você pode usar o método [ICorDebugILFrame:: GetIP](icordebugilframe-getip-method.md) para obter o valor do ponteiro de instrução.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
