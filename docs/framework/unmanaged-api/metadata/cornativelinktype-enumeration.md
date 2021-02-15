---
description: 'Saiba mais sobre: Enumeração CorNativeLinkType'
title: Enumeração CorNativeLinkType
ms.date: 03/30/2017
api_name:
- CorNativeLinkType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorNativeLinkType
helpviewer_keywords:
- CorNativeLinkType enumeration [.NET Framework metadata]
ms.assetid: 4f86ff37-2dab-4e64-819a-76b3bfe828ff
topic_type:
- apiref
ms.openlocfilehash: 40efc75a793da8b024eff3d7c2c620123eca08b2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784334"
---
# <a name="cornativelinktype-enumeration"></a>Enumeração CorNativeLinkType

Fornece valores que indicam o tipo vinculado em código nativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum
{  
    nltNone       = 1,  
    nltAnsi       = 2,  
    nltUnicode    = 3,  
    nltAuto       = 4,  
    nltOle        = 5,  
    nltMaxValue   = 7  
} CorNativeLinkType;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`nltNone`|Indica que nenhuma das palavras-chave está especificada.|  
|`nltAnsi`|Indica que uma palavra-chave ANSI está especificada.|  
|`nltUnicode`|Indica que uma palavra-chave Unicode está especificada|  
|`nltAuto`|Indica que uma palavra-chave auto está especificada.|  
|`nltOle`|Indica que uma palavra-chave OLE está especificada.|  
|`nltMaxValue`|Não usado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
