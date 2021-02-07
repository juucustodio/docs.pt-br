---
description: 'Saiba mais sobre o método: ICLRDataTarget2:: FreeVirtual'
title: Método ICLRDataTarget2::FreeVirtual
ms.date: 03/30/2017
api_name:
- ICLRDataTarget2.FreeVirtual
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget2::FreeVirtual
helpviewer_keywords:
- ICLRDataTarget::FreeVirtual method [.NET Framework debugging]
- FreeVirtual method [.NET Framework debugging]
ms.assetid: 26fb69f8-1467-4711-bd24-cb117c63938f
topic_type:
- apiref
ms.openlocfilehash: ef4048f421fcdc7d284663036f8cc9f2614f4e13
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729239"
---
# <a name="iclrdatatarget2freevirtual-method"></a>Método ICLRDataTarget2::FreeVirtual

Chamado pelos serviços de acesso a dados do Common Language Runtime (CLR) para liberar memória que foi alocada anteriormente no espaço de endereço do processo de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FreeVirtual(  
    [in] CLRDATA_ADDRESS addr,  
    [in] ULONG32 size,  
    [in] ULONG32 typeFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `addr`  
 no Um `CLRDATA_ADDRESS` valor que especifica o endereço inicial da memória a ser liberada.  
  
 `size`  
 no O tamanho, em bytes, da memória a ser liberada.  
  
 `typeFlags`  
 no Sinalizadores que controlam a liberação de memória. Consulte a função do Win32 `VirtualFree` .  
  
## <a name="remarks"></a>Comentários  

 O `FreeVirtual` método serve como um wrapper lógico para a função do Win32 `VirtualFree` .  
  
 Este método é implementado pelo autor do aplicativo de depuração.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRDataTarget2](iclrdatatarget2-interface.md)
- [Método AllocVirtual](iclrdatatarget2-allocvirtual-method.md)
