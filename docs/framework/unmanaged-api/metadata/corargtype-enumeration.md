---
description: 'Saiba mais sobre: Enumeração CorArgType'
title: Enumeração CorArgType
ms.date: 03/30/2017
api_name:
- CorArgType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorArgType
helpviewer_keywords:
- CorArgType enumeration [.NET Framework metadata]
ms.assetid: 3c1cb268-57a0-4664-91c7-f6908ff29e32
topic_type:
- apiref
ms.openlocfilehash: de7067e6c7b825aae797d88dbd5f2ecd2f5280fa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99678517"
---
# <a name="corargtype-enumeration"></a>Enumeração CorArgType

Contém valores que descrevem o tipo nativo de um identificador de tempo de execução.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef enum CorArgType {  
  
    IMAGE_CEE_CS_END        = 0x0,  
    IMAGE_CEE_CS_VOID       = 0x1,  
    IMAGE_CEE_CS_I4         = 0x2,  
    IMAGE_CEE_CS_I8         = 0x3,  
    IMAGE_CEE_CS_R4         = 0x4,  
    IMAGE_CEE_CS_R8         = 0x5,  
    IMAGE_CEE_CS_PTR        = 0x6,  
    IMAGE_CEE_CS_OBJECT     = 0x7,  
    IMAGE_CEE_CS_STRUCT4    = 0x8,  
    IMAGE_CEE_CS_STRUCT32   = 0x9,  
    IMAGE_CEE_CS_BYVALUE    = 0xA  
  
} CorArgType;  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
