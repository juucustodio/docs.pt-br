---
description: 'Saiba mais sobre: enumeração CorPropertyAttr'
title: Enumeração CorPropertyAttr
ms.date: 03/30/2017
api_name:
- CorPropertyAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorPropertyAttr
helpviewer_keywords:
- CorPropertyAttr enumeration [.NET Framework metadata]
ms.assetid: 58ac8202-854d-4efd-acfb-d2da8b446e12
topic_type:
- apiref
ms.openlocfilehash: 1f3e2fccb11a067c6c46350a2c36d47007875755
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784230"
---
# <a name="corpropertyattr-enumeration"></a>Enumeração CorPropertyAttr

Contém valores que descrevem os metadados de uma propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorPropertyAttr {  
  
    prSpecialName           =   0x0200,
    prReservedMask          =   0xf400,  
    prRTSpecialName         =   0x0400,  
    prHasDefault            =   0x1000,  
    prUnused                =   0xe9ff  
  
} CorPropertyAttr;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`prSpecialName`|Especifica que a propriedade é especial e que seu nome descreve como.|  
|`prReservedMask`|Reservado para uso interno pelo Common Language Runtime.|  
|`prRTSpecialName`|Especifica que os Common Language Runtime APIs internas de metadados devem verificar a codificação do nome da propriedade.|  
|`prHasDefault`|Especifica que a propriedade tem um valor padrão.|  
|`prUnused`|Não utilizado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
