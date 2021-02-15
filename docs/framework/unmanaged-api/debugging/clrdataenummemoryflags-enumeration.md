---
description: 'Saiba mais sobre: Enumeração CLRDataEnumMemoryFlags'
title: Enumeração CLRDataEnumMemoryFlags
ms.date: 03/30/2017
api_name:
- CLRDataEnumMemoryFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CLRDataEnumMemoryFlags
helpviewer_keywords:
- CLRDataEnumMemoryFlags enumeration [.NET Framework debugging]
ms.assetid: e249f9fc-e24a-4506-903c-92781f6eab7c
topic_type:
- apiref
ms.openlocfilehash: 3522649c59177de8295416ce260c374df605efb3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662215"
---
# <a name="clrdataenummemoryflags-enumeration"></a>Enumeração CLRDataEnumMemoryFlags

Indica quais regiões de memória uma chamada para o método [ICLRDataEnumMemoryRegions:: EnumMemoryRegions](iclrdataenummemoryregions-enummemoryregions-method.md) deve incluir.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CLRDataEnumMemoryFlags {  
    CLRDATA_ENUM_MEM_DEFAULT  = 0x0,  
    CLRDATA_ENUM_MEM_MINI     = CLRDATA_ENUM_MEM_DEFAULT,  
    CLRDATA_ENUM_MEM_HEAP     = 0x1  
} CLRDataEnumMemoryFlags;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`CLRDATA_ENUM_MEM_DEFAULT`|Um minidespejo, ou seja, um despejo de memória esparso.|  
|`CLRDATA_ENUM_MEM_HEAP`|Um despejo de pilha completo.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
