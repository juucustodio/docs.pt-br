---
description: 'Saiba mais sobre o método: ISymUnmanagedConstant:: getsignature'
title: Método ISymUnmanagedConstant::GetSignature
ms.date: 03/30/2017
api_name:
- ISymUnmanagedConstant.GetSignature
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedConstant::GetSignature
helpviewer_keywords:
- GetSignature method, ISymUnmanagedConstant interface [.NET Framework debugging]
- ISymUnmanagedConstant::GetSignature method [.NET Framework debugging]
ms.assetid: 3eb41151-a228-43e3-ba8f-e6dd3ceb8542
topic_type:
- apiref
ms.openlocfilehash: d28051c9d0e2675e980926fe63ffa7c4d13ef13a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689788"
---
# <a name="isymunmanagedconstantgetsignature-method"></a>Método ISymUnmanagedConstant::GetSignature

Obtém a assinatura da constante.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSignature(  
    [in]  ULONG32  cSig,  
    [out] ULONG32  *pcSig,  
    [out, size_is(cSig),  
        length_is(*pcSig)] BYTE sig[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cSig`  
 no O comprimento do buffer para o qual o `pcSig` parâmetro aponta.  
  
 `pcSig`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em caracteres, do buffer necessário para conter a assinatura.  
  
 `sig`  
 fora O buffer que armazena a assinatura.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedConstant](isymunmanagedconstant-interface.md)
- [Método GetName](isymunmanagedconstant-getname-method.md)
- [Método GetValue](isymunmanagedconstant-getvalue-method.md)
