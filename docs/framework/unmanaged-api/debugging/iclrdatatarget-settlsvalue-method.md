---
description: 'Saiba mais sobre o método: ICLRDataTarget:: SetTLSValue'
title: Método ICLRDataTarget::SetTLSValue
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.SetTLSValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::SetTLSValue
helpviewer_keywords:
- ICLRDataTarget::SetTLSValue method [.NET Framework debugging]
- SetTLSValue method [.NET Framework debugging]
ms.assetid: 4a2d6a24-749a-47ad-9f01-4517203d3f35
topic_type:
- apiref
ms.openlocfilehash: 2432cd66f604575e35f171c98a0fb313c5ccd94e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785673"
---
# <a name="iclrdatatargetsettlsvalue-method"></a>Método ICLRDataTarget::SetTLSValue

Define um valor no armazenamento local de threads (TLS) do thread especificado no processo de destino. Esse método é chamado pelos serviços de acesso a dados do Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetTLSValue (  
    [in] ULONG32            threadID,  
    [in] ULONG32            index,  
    [in] CLRDATA_ADDRESS    value  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `threadID`  
 no O identificador do sistema operacional de um thread no processo de destino.  
  
 `index`  
 no O índice do local. Esse valor deve ser um índice válido no repositório local do thread especificado.  
  
 `value`  
 no Um `CLRDATA_ADDRESS` valor que especifica o valor a ser colocado no local de TLS fornecido.  
  
## <a name="remarks"></a>Comentários  

 Este método é implementado pelo autor do aplicativo de depuração.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRDataTarget](iclrdatatarget-interface.md)
