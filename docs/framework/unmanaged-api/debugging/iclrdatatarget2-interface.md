---
description: 'Saiba mais sobre: interface ICLRDataTarget2'
title: Interface ICLRDataTarget2
ms.date: 03/30/2017
api_name:
- ICLRDataTarget2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget2
helpviewer_keywords:
- ICLRDataTarget2 interface [.NET Framework debugging]
ms.assetid: 94249397-861b-4294-a538-cf01466a66d3
topic_type:
- apiref
ms.openlocfilehash: 9ba6d11ea043d3b6ba85544b47e063f585854af8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794839"
---
# <a name="iclrdatatarget2-interface"></a>Interface ICLRDataTarget2

Uma subclasse de [ICLRDataTarget](iclrdatatarget-interface.md) que é usada pela camada de serviços de acesso a dados para manipular regiões de memória virtual no processo de destino.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método AllocVirtual](iclrdatatarget2-allocvirtual-method.md)|Aloca memória no espaço de endereço do processo de destino.|  
|[Método FreeVirtual](iclrdatatarget2-freevirtual-method.md)|Libera a memória que foi alocada anteriormente no espaço de endereço do processo de destino.|  
  
## <a name="remarks"></a>Comentários  

 O cliente da API (ou seja, o depurador) deve implementar a interface conforme o apropriado para o processo de destino específico. Por exemplo, um processo dinâmico teria uma implementação diferente da implementação de um despejo de memória. O destino pode não oferecer suporte à modificação de suas regiões de memória.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRDataTarget](iclrdatatarget-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
