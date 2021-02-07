---
description: 'Saiba mais sobre: método ISymUnmanagedConstant:: GetValue'
title: Método ISymUnmanagedConstant::GetValue
ms.date: 03/30/2017
api_name:
- ISymUnmanagedConstant.GetValue
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedConstant::GetValue
helpviewer_keywords:
- GetValue method, ISymUnmanagedConstant interface [.NET Framework debugging]
- ISymUnmanagedConstant::GetValue method [.NET Framework debugging]
ms.assetid: 0036fc10-e768-47a8-b9cf-bf47faf8d194
topic_type:
- apiref
ms.openlocfilehash: 05818028deb804bf2a2426285b5185b01776199d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689684"
---
# <a name="isymunmanagedconstantgetvalue-method"></a>Método ISymUnmanagedConstant::GetValue

 Obtém o valor da constante.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetValue(  
    [out]  VARIANT* pValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pValue`  
 fora Um ponteiro para uma variável que recebe o valor.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedConstant](isymunmanagedconstant-interface.md)
- [Método GetName](isymunmanagedconstant-getname-method.md)
- [Método GetSignature](isymunmanagedconstant-getsignature-method.md)
