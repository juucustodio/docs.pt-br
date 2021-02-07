---
description: 'Saiba mais sobre o método: ICLRDataTarget2:: AllocVirtual'
title: Método ICLRDataTarget2::AllocVirtual
ms.date: 03/30/2017
api_name:
- ICLRDataTarget2.AllocVirtual
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget2::AllocVirtual
helpviewer_keywords:
- ICLRDataTarget2::AllocVirtual method [.NET Framework debugging]
- AllocVirtual method [.NET Framework debugging]
ms.assetid: e3226230-964b-47fb-9f53-d6fdbeda1e9e
topic_type:
- apiref
ms.openlocfilehash: d81474e4067599178285b6fa876919298617919d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729322"
---
# <a name="iclrdatatarget2allocvirtual-method"></a>Método ICLRDataTarget2::AllocVirtual

Chamado pelos serviços de acesso a dados do Common Language Runtime (CLR) para alocar memória no espaço de endereço desse processo de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AllocVirtual(  
    [in] CLRDATA_ADDRESS addr,  
    [in] ULONG32 size,  
    [in] ULONG32 typeFlags,  
    [in] ULONG32 protectFlags,  
    [out] CLRDATA_ADDRESS* virt  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `addr`  
 no Um `CLRDATA_ADDRESS` valor que especifica o endereço inicial solicitado da memória a ser alocada.  
  
 `size`  
 no O tamanho, em bytes, da memória a ser alocada.  
  
 `typeFlags`  
 no Sinalizadores que controlam a alocação de memória. Consulte a função do Win32 `VirtualAlloc` .  
  
 `protectFlags`  
 no Os atributos de proteção para a memória alocada. Consulte a função do Win32 `VirtualAlloc` .  
  
 `virt`  
 fora Um ponteiro para um `CLRDATA_ADDRESS` valor que especifica o endereço inicial real da memória alocada.  
  
## <a name="remarks"></a>Comentários  

 O `AllocVirtual` método serve como um wrapper lógico para a função do Win32 `VirtualAlloc` .  
  
 Este método é implementado pelo autor do aplicativo de depuração.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRDataTarget2](iclrdatatarget2-interface.md)
- [Método FreeVirtual](iclrdatatarget2-freevirtual-method.md)
