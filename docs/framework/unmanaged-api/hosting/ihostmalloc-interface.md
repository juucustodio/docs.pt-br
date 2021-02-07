---
description: 'Saiba mais sobre: interface IHostMalloc'
title: Interface IHostMalloc
ms.date: 03/30/2017
api_name:
- IHostMAlloc
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMAlloc
helpviewer_keywords:
- IHostMAlloc interface [.NET Framework hosting]
ms.assetid: e3c6643b-6fc7-4a99-959d-4b7b4e63fdee
topic_type:
- apiref
ms.openlocfilehash: cd04a0f71fd429ea10b9edcce02806f4afa57148
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99708171"
---
# <a name="ihostmalloc-interface"></a>Interface IHostMalloc

Fornece métodos que permitem que o Common Language Runtime (CLR) solicite alocações refinadas do heap por meio do host.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Alloc](ihostmalloc-alloc-method.md)|Solicita que o host aloque a quantidade solicitada de memória do heap.|  
|[Método DebugAlloc](ihostmalloc-debugalloc-method.md)|Solicita que o host aloque a quantidade solicitada de memória do heap e rastreie também onde a memória foi alocada.|  
|[Método Free](ihostmalloc-free-method.md)|Libera a memória que foi alocada usando o `Alloc` método.|  
  
## <a name="remarks"></a>Comentários  

 O CLR Obtém um ponteiro de interface para uma `IHostMalloc` instância chamando o método [IHostMemoryManager:: CreateMAlloc](ihostmemorymanager-createmalloc-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostMemoryManager](ihostmemorymanager-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
