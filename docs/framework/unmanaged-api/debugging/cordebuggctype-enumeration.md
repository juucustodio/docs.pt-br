---
description: 'Saiba mais sobre: Enumeração CorDebugGCType'
title: Enumeração CorDebugGCType
ms.date: 03/30/2017
api_name:
- CorDebugGCType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugGCType
helpviewer_keywords:
- CorDebugGCType enumeration [.NET Framework debugging]
ms.assetid: 880ca92a-42d4-42a5-9b9c-c2848eb39c6a
topic_type:
- apiref
ms.openlocfilehash: 4be835a9a028a882fa050991beb31d2a8dec5354
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801651"
---
# <a name="cordebuggctype-enumeration"></a>Enumeração CorDebugGCType

Indica se o coletor de lixo está sendo executado em uma estação de trabalho ou em um servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugGCType {  
    CorDebugWorkstationGC  = 0,  
    CorDebugServerGC       = ( CorDebugWorkstationGC + 1 )  
} CorDebugGCType;  
```  
  
## <a name="parameters"></a>Parâmetros  
  
## <a name="members"></a>Membros  
  
|Nome do membro|Descrição|  
|-----------------|-----------------|  
|`CorDebugWorkstationGC`|O coletor de lixo está em execução em uma estação de trabalho.|  
|`CorDebugServerGC`|O coletor de lixo está em execução em um servidor.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
