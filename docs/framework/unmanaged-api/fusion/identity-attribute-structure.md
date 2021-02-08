---
description: 'Saiba mais sobre: estrutura de IDENTITY_ATTRIBUTE'
title: Estrutura IDENTITY_ATTRIBUTE
ms.date: 03/30/2017
api_name:
- IDENTITY_ATTRIBUTE
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IDENTITY_ATTRIBUTE
helpviewer_keywords:
- IDENTITY_ATTRIBUTE structure [.NET Framework fusion]
ms.assetid: 1ee7c434-9681-4fa8-badd-652cb1a9742b
topic_type:
- apiref
ms.openlocfilehash: 52610961ab202fc79351073eac1846a1a63889e3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800169"
---
# <a name="identity_attribute-structure"></a>Estrutura IDENTITY_ATTRIBUTE

Contém informações de atributo de metadados sobre uma instância de [IDefinitionIdentity](idefinitionidentity-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _IDENTITY_ATTRIBUTE {  
    LPCWSTR  pszNamespace;  
    LPCWSTR  pszName;  
    LPCWSTR  pszValue;  
} IDENTITY_ATTRIBUTE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`pszNamespace`|Um ponteiro para uma cadeia de caracteres de caractere terminada em nulo que contém o namespace no qual o atributo está.|  
|`pszName`|Um ponteiro para uma cadeia de caracteres de caractere terminada em nulo que contém o nome do atributo.|  
|`pszValue`|Um ponteiro para uma cadeia de caracteres de caractere terminada em nulo que contém o valor do atributo.|  
  
## <a name="remarks"></a>Comentários  

 A `IDENTITY_ATTRIBUTE` estrutura contém três ponteiros para cadeias de caracteres terminadas em nulo. Essas três cadeias de caracteres descrevem um atributo.  
  
 Uma instância de uma `IDENTITY_ATTRIBUTE` estrutura é associada a uma instância de uma estrutura de [IDENTITY_ATTRIBUTE_BLOB](identity-attribute-blob-structure.md) . A `IDENTITY_ATTRIBUTE` estrutura contém as cadeias de caracteres reais e a `IDENTITY_ATTRIBUTE_BLOB` estrutura correspondente lista os deslocamentos para as três cadeias de caracteres listadas na `IDENTITY_ATTRIBUTE` estrutura.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Isolamento. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IDefinitionIdentity](idefinitionidentity-interface.md)
- [Estrutura IDENTITY_ATTRIBUTE_BLOB](identity-attribute-blob-structure.md)
- [Estruturas de fusão](fusion-structures.md)
