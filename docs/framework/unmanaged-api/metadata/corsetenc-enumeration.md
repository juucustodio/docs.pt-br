---
description: 'Saiba mais sobre: Enumeração CorSetENC'
title: Enumeração CorSetENC
ms.date: 03/30/2017
api_name:
- CorSetENC
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSetENC
helpviewer_keywords:
- CorSetENC enumeration [.NET Framework metadata]
ms.assetid: fe4150e8-071d-43fb-8e06-c3c616dbeed2
topic_type:
- apiref
ms.openlocfilehash: 5ba3e41c10b082ceb2ce7d327f7ff7f857ca98a5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99707391"
---
# <a name="corsetenc-enumeration"></a>Enumeração CorSetENC

Contém valores usados para influenciar o comportamento durante a geração de metadados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorSetENC {  
  
    MDSetENCOn                  = 0x00000001,  
    MDSetENCOff                 = 0x00000002,  
  
    MDUpdateENC                 = 0x00000001,  
    MDUpdateFull                = 0x00000002,  
    MDUpdateExtension           = 0x00000003,  
    MDUpdateIncremental         = 0x00000004,  
    MDUpdateDelta               = 0x00000005,  
    MDUpdateMask                = 0x00000007  
  
} CorSetENC;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`MDSetENCOn`|Obsoleto.|  
|`MDSetENCOff`|Obsoleto.|  
|`MDUpdateENC`|Indica que, enquanto os metadados podem ser atualizados, os tokens não podem ser movidos.|  
|`MDUpdateFull`|Indica que os tokens podem ser movidos durante as atualizações.|  
|`MDUpdateExtension`|Indica que as atualizações podem consistir apenas em adições. Tokens não podem ser movidos.|  
|`MDUpdateIncremental`|Indica que a compilação é incremental.|  
|`MDUpdateDelta`|Indica que somente os metadados alterados devem ser salvos.|  
|`MDUpdateMask`|Inclui `MDUpdateENC` o `MDUpdateFull` e o `MDUpdateIncremental` .|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
