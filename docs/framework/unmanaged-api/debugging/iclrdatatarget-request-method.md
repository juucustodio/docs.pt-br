---
description: 'Saiba mais sobre o método: ICLRDataTarget:: Request'
title: Método ICLRDataTarget::Request
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.Request
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::Request
helpviewer_keywords:
- ICLRDataTarget::Request method [.NET Framework debugging]
- Request method [.NET Framework debugging]
ms.assetid: 4723bd1c-eddb-4ed2-897a-010024a47e01
topic_type:
- apiref
ms.openlocfilehash: 75c400a51a2fdaf0044d85b5f483d783fae4628b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712149"
---
# <a name="iclrdatatargetrequest-method"></a>Método ICLRDataTarget::Request

Chamado pelos serviços de acesso a dados do Common Language Runtime (CLR) para solicitar uma operação, conforme definido pela implementação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Request (  
    [in] ULONG32            reqCode,  
    [in] ULONG32            inBufferSize,  
    [in, size_is(inBufferSize)]
        BYTE                *inBuffer,  
    [in] ULONG32            outBufferSize,  
    [out, size_is(outBufferSize)]
        BYTE                *outBuffer  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `reqCode`  
 no Definido pelo usuário.  
  
 `inBufferSize`  
 no O tamanho do buffer de entrada, que é usado para a solicitação de entrada.  
  
 `inBuffer`  
 no Um buffer que contém a solicitação.  
  
 `outBufferSize`  
 no O tamanho do buffer de saída, que é usado para a resposta.  
  
 `outBuffer`  
 fora Um buffer que contém a resposta.  
  
## <a name="remarks"></a>Comentários  

 O `Request` método facilita a adição de operações personalizadas não especificadas. Ou seja, esse método fornece extensibilidade sem exigir a revisão da definição da interface.  
  
 Este método é implementado pelo autor do aplicativo de depuração.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRDataTarget](iclrdatatarget-interface.md)
