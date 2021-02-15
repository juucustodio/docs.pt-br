---
description: 'Saiba mais sobre: Enumeração CorFileFlags'
title: Enumeração CorFileFlags
ms.date: 03/30/2017
api_name:
- CorFileFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorFileFlags
helpviewer_keywords:
- CorFileFlags enumeration [.NET Framework metadata]
ms.assetid: d16703fd-518f-412e-92cb-74433d11032e
topic_type:
- apiref
ms.openlocfilehash: 8ffad9bad9c656a10c2c556f5e06f9d510ccb45a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784477"
---
# <a name="corfileflags-enumeration"></a>Enumeração CorFileFlags

Contém valores que descrevem o tipo de arquivo definido em uma chamada para [IMetaDataAssemblyEmit::D efinefile](imetadataassemblyemit-definefile-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorFileFlags {  
  
    ffContainsMetaData      =   0x0000,  
    ffContainsNoMetaData    =   0x0001  
  
} CorFileFlags;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`ffContainsMetaData`|Indica que o arquivo não é um arquivo de recurso.|  
|`ffContainsNoMetaData`|Indica que o arquivo, possivelmente um arquivo de recurso, não contém metadados.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
