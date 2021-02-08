---
description: 'Saiba mais sobre: enumeração CorMethodSemanticsAttr'
title: Enumeração CorMethodSemanticsAttr
ms.date: 03/30/2017
api_name:
- CorMethodSemanticsAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorMethodSemanticsAttr
helpviewer_keywords:
- CorMethodSemanticsAttr enumeration [.NET Framework metadata]
ms.assetid: ca2af325-eb9d-4a91-90e4-267e45b98611
topic_type:
- apiref
ms.openlocfilehash: 4079e81ae2389ff0684fd11d0751b191a7289932
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784360"
---
# <a name="cormethodsemanticsattr-enumeration"></a>Enumeração CorMethodSemanticsAttr

Contém valores que descrevem a relação entre um método e uma propriedade ou evento associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorMethodSemanticsAttr {  
  
    msSetter    =   0x0001,  
    msGetter    =   0x0002,  
    msOther     =   0x0004,  
    msAddOn     =   0x0008,  
    msRemoveOn  =   0x0010,  
    msFire      =   0x0020,  
  
} CorMethodSemanticsAttr;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`msSetter`|Especifica que o método é um `set` acessador para uma propriedade.|  
|`msGetter`|Especifica que o método é um `get` acessador para uma propriedade.|  
|`msOther`|Especifica que o método tem uma relação com uma propriedade ou um evento diferente daqueles definidos aqui.|  
|`msAddOn`|Especifica que o método adiciona métodos de manipulador para um evento.|  
|`msRemoveOn`|Especifica que o método Remove métodos de manipulador para um evento.|  
|`msFire`|Especifica que o método gera um evento.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
