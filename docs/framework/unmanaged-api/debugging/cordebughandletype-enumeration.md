---
description: 'Saiba mais sobre: Enumeração CorDebugHandleType'
title: Enumeração CorDebugHandleType
ms.date: 03/30/2017
api_name:
- CorDebugHandleType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugHandleType
helpviewer_keywords:
- CorDebugHandleType enumeration [.NET Framework debugging]
ms.assetid: 84296b55-c2c5-424c-ac9c-8e28e2895945
topic_type:
- apiref
ms.openlocfilehash: 294fd7b04018331489e51d12930bcbbb81ec340a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662111"
---
# <a name="cordebughandletype-enumeration"></a>Enumeração CorDebugHandleType

Indica o tipo de manipulação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugHandleType {  
    HANDLE_STRONG                  = 1,  
    HANDLE_WEAK_TRACK_RESURRECTION = 2  
} CorDebugHandleType;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`HANDLE_STRONG`|O identificador é forte, o que impede que um objeto seja recuperado pela coleta de lixo.|  
|`HANDLE_WEAK_TRACK_RESURRECTION`|O identificador é fraco, o que não impede que um objeto seja recuperado pela coleta de lixo.<br /><br /> O identificador torna-se inválido quando o objeto é coletado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
