---
title: Interface ICLRGCManager2
ms.date: 03/30/2017
api_name:
- ICLRGCManager2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager2
helpviewer_keywords:
- ICLRGCManager2 interface [.NET Framework hosting]
ms.assetid: 4b5ffd7b-9ad7-41cd-9bba-34030ae3da7e
topic_type:
- apiref
ms.openlocfilehash: 0f3ecc0d497eaee937647df47ba0956335a2fe41
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703948"
---
# <a name="iclrgcmanager2-interface"></a>Interface ICLRGCManager2
Fornece métodos que permitem que um host interaja com o sistema de coleta de lixo do Common Language Runtime.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método SetGCStartupLimitsEx](iclrgcmanager2-setgcstartuplimitsex-method.md)|Define o tamanho de um segmento de coleta de lixo e o tamanho máximo da geração 0 do sistema de coleta de lixo. Habilita a geração 0 e os tamanhos de segmento maiores que `DWORD` .|  
  
## <a name="remarks"></a>Comentários  
 Essa interface herda da [interface ICLRGCManager](iclrgcmanager-interface.md).  
  
 O Common Language Runtime (CLR) implementa seu mecanismo de coleta de lixo com o <xref:System.GC> tipo gerenciado. Para obter mais informações sobre o sistema de coleta de lixo, consulte [coleta de lixo](../../../standard/garbage-collection/index.md).  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso em MSCorEE. dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Veja também

- [Gerenciamento automático de memória](../../../standard/automatic-memory-management.md)
- [Estrutura COR_GC_STATS](cor-gc-stats-structure.md)
- [Interface ICLRControl](iclrcontrol-interface.md)
- [Interfaces de hospedagem CLR adicionadas ao .NET Framework 4 e 4.5](clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
