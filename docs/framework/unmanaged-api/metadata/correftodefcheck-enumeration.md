---
description: 'Saiba mais sobre: Enumeração CorRefToDefCheck'
title: Enumeração CorRefToDefCheck
ms.date: 03/30/2017
api_name:
- CorRefToDefCheck
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorRefToDefCheck
helpviewer_keywords:
- CorRefToDefCheck enumeration [.NET Framework metadata]
ms.assetid: f9a80f1a-55af-4459-b095-8441aae16119
topic_type:
- apiref
ms.openlocfilehash: ca9d1c7ceb3d9f82ef8d5f1f54d869db64053e69
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784243"
---
# <a name="correftodefcheck-enumeration"></a>Enumeração CorRefToDefCheck

Especifica sinalizadores para controlar quais itens referenciados são convertidos em suas definições a fim de otimizar o código.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorRefToDefCheck {  
    MDRefToDefDefault           = 0x00000003,  
    MDRefToDefAll               = 0xffffffff,  
    MDRefToDefNone              = 0x00000000,  
    MDTypeRefToDef              = 0x00000001,  
    MDMemberRefToDef            = 0x00000002  
} CorRefToDefCheck;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`MDRefToDefDefault`|Especifica que referências de tipo e referências de membro devem ser convertidas em definições. Esse é o valor padrão ( `MDTypeRefToDef` &#124; `MDMemberRefToDef` ).|  
|`MDRefToDefAll`|Especifica que todos os itens referenciados devem ser convertidos em definições.|  
|`MDRefToDefNone`|Especifica que nenhum item referenciado deve ser convertido em definições.|  
|`MDTypeRefToDef`|Especifica que apenas referências de tipo devem ser convertidas em definições de tipo.|  
|`MDMemberRefToDef`|Especifica que somente referências de membro devem ser convertidas em definições. Ou seja, as referências de membro devem ser convertidas em definições de método ou definições de campo.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
