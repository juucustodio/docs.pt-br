---
description: 'Saiba mais sobre: estrutura de COR_TYPE_LAYOUT'
title: Estrutura COR_TYPE_LAYOUT
ms.date: 03/30/2017
api_name:
- COR_TYPE_LAYOUT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_TYPE_LAYOUT
helpviewer_keywords:
- COR_TYPE_LAYOUT structure [.NET Framework debugging]
ms.assetid: 43a7addd-f25a-4049-9907-abec3eb17af2
topic_type:
- apiref
ms.openlocfilehash: 07bed0c526aae38cb380b57da505a3f02bdf4aae
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801758"
---
# <a name="cor_type_layout-structure"></a>Estrutura COR_TYPE_LAYOUT

Fornece informações sobre o layout de um objeto na memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct COR_TYPE_LAYOUT {  
    COR_TYPEID parentID;  
    ULONG32 objectSize;  
    ULONG32 numFields;  
    ULONG32 boxOffset;  
    CorElementType type;  
} COR_TYPE_LAYOUT;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`parentID`|O identificador do tipo pai para esse tipo. Essa será a ID de tipo nulo (token1 = 0, token2 = 0) se a ID de tipo corresponder a <xref:System.Object?displayProperty=nameWithType> .|  
|`objectSize`|O tamanho de base de um objeto deste tipo. Este é o tamanho total para objetos que não são de tamanho variável.|  
|`numFields`|O número de campos incluídos em objetos deste tipo.|  
|`boxOffset`|Se esse tipo for in box, o deslocamento inicial dos campos de um objeto. Esse campo é válido somente para tipos de valor como primitivos e estruturas.|  
|`type`|O CorElementType ao qual esse tipo pertence.|  
  
## <a name="remarks"></a>Comentários  

 Se `numFields` for maior que zero, você poderá chamar o método [ICorDebugProcess5:: GetTypeFields](icordebugprocess5-gettypefields-method.md) para obter informações sobre os campos nesse tipo. Se `type` for `ELEMENT_TYPE_STRING` , `ELEMENT_TYPE_ARRAY` , ou `ELEMENT_TYPE_SZARRAY` , o tamanho dos objetos desse tipo é variável e você pode passar a estrutura de [COR_TYPEID](cor-typeid-structure.md) para o método [ICorDebugProcess5:: GetArrayLayout](icordebugprocess5-getarraylayout-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
