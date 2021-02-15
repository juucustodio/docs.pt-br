---
description: 'Saiba mais sobre: Enumeração CorDebugJITCompilerFlags'
title: Enumeração CorDebugJITCompilerFlags
ms.date: 03/30/2017
api_name:
- CorDebugJITCompilerFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugJITCompilerFlags
helpviewer_keywords:
- CorDebugJITCompilerFlags enumeration [.NET Framework debugging]
ms.assetid: c0774f70-5bed-45e8-9922-fdad778c4c33
topic_type:
- apiref
ms.openlocfilehash: 7e5337293aa4fe446deb12653acd22864eb7679a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801599"
---
# <a name="cordebugjitcompilerflags-enumeration"></a>Enumeração CorDebugJITCompilerFlags

Contém valores que influenciam o comportamento do compilador just-in-time (JIT) gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugJITCompilerFlags {  
  
    CORDEBUG_JIT_DEFAULT = 0x1,  
    CORDEBUG_JIT_DISABLE_OPTIMIZATION = 0x3,  
    CORDEBUG_JIT_ENABLE_ENC = 0x7  
  
} CorDebugJITCompilerFlags;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`CORDEBUG_JIT_DEFAULT`|Especifica que o compilador deve controlar os dados de compilação e permite otimizações.|  
|`CORDEBUG_JIT_DISABLE_OPTIMIZATION`|Especifica que o compilador deve controlar os dados de compilação, mas desabilita otimizações.|  
|`CORDEBUG_JIT_ENABLE_ENC`|Especifica que o compilador deve controlar os dados de compilação, desabilitar otimizações e habilitar as tecnologias editar e continuar.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
