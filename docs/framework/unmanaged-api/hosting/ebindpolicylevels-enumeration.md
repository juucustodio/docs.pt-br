---
description: 'Saiba mais sobre: Enumeração EBindPolicyLevels'
title: Enumeração EBindPolicyLevels
ms.date: 03/30/2017
api_name:
- EBindPolicyLevels
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EBindPolicyLevels
helpviewer_keywords:
- EBindPolicyLevels enumeration [.NET Framework hosting]
ms.assetid: a9e00b4f-b6d0-4257-bd88-4fe9af97b8fa
topic_type:
- apiref
ms.openlocfilehash: 00e10cff79cdd782e8d9ab8e9b7e1e3f388fb1ee
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785608"
---
# <a name="ebindpolicylevels-enumeration"></a>Enumeração EBindPolicyLevels

Fornece sinalizadores para especificar o nível no qual aplicar ou modificar a política de assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    ePolicyLevelNone         = 0x0,  
    ePolicyLevelRetargetable = 0x1,  
    ePolicyUnifiedToCLR      = 0x2,  
    ePolicyLevelApp          = 0x4,  
    ePolicyLevelPublisher    = 0x8,  
    ePolicyLevelHost         = 0x10,  
    ePolicyLevelAdmin        = 0x20  
    ePolicyPortability       = 0x40  
} EBindPolicyLevels;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`ePolicyLevelAdmin`|Especifica que a política deve ser aplicada no nível de administrador.|  
|`ePolicyLevelApp`|Especifica que a política deve ser aplicada no nível do aplicativo.|  
|`ePolicyLevelHost`|Especifica que a política deve ser aplicada no nível do host.|  
|`ePolicyLevelNone`|Especifica nenhum sinalizador de nível de política.|  
|`ePolicyLevelPublisher`|Especifica que a política deve ser aplicada no nível do Publicador.|  
|`ePolicyLevelRetargetable`|Especifica que a política deve ser aplicável em níveis de variável.|  
|`ePolicyPortability`|Especifica que a política deve dar suporte à portabilidade entre as implementações de um assembly .NET Framework. Consulte o [\<supportPortability>](../../configure-apps/file-schema/runtime/supportportability-element.md) elemento arquivo de configuração.|  
|`ePolicyUnifiedToCLR`|Especifica que a política deve ser unificada para a do Common Language Runtime (CLR).|  
  
## <a name="remarks"></a>Comentários  

 Essa enumeração é passada para métodos da interface [ICLRHostBindingPolicyManager](iclrhostbindingpolicymanager-interface.md) para especificar alterações na política de aplicativo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
