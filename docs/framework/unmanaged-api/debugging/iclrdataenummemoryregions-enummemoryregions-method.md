---
description: 'Saiba mais sobre o método: ICLRDataEnumMemoryRegions:: EnumMemoryRegions'
title: Método ICLRDataEnumMemoryRegions::EnumMemoryRegions
ms.date: 03/30/2017
api_name:
- ICLRDataEnumMemoryRegions.EnumMemoryRegions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataEnumMemoryRegions::EnumMemoryRegions
helpviewer_keywords:
- ICLRDataEnumMemoryRegions::EnumMemoryRegions method [.NET Framework debugging]
- EnumMemoryRegions method [.NET Framework debugging]
ms.assetid: 22d2e339-f174-40b5-a478-0b744501566f
topic_type:
- apiref
ms.openlocfilehash: 48887defab38d6ac99c718e14646d39166927438
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785712"
---
# <a name="iclrdataenummemoryregionsenummemoryregions-method"></a>Método ICLRDataEnumMemoryRegions::EnumMemoryRegions

Enumera áreas especificadas de memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumMemoryRegions (  
    [in] ICLRDataEnumMemoryRegionsCallback  *callback,  
    [in] ULONG32                            miniDumpFlags,  
    [in] CLRDataEnumMemoryFlags             clrFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `callback`  
 no Um ponteiro para uma instância de [ICLRDataEnumMemoryRegionsCallback](iclrdataenummemoryregionscallback-interface.md) que é chamada por esse método para cada região de memória que está sendo enumerada para notificar o depurador do resultado.  
  
 A enumeração de regiões de memória continua mesmo que o retorno de chamada indique uma falha.  
  
 `miniDumpFlags`  
 no Não usado.  
  
 `clrFlags`  
 no Um valor da enumeração [CLRDataEnumMemoryFlags](clrdataenummemoryflags-enumeration.md) que especifica as regiões de memória a serem enumeradas.  
  
## <a name="remarks"></a>Comentários  

 Esse método usa a instância [ICLRDataEnumMemoryRegionsCallback](iclrdataenummemoryregionscallback-interface.md) especificada para notificar o chamador de resultados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRDataEnumMemoryRegions](iclrdataenummemoryregions-interface.md)
