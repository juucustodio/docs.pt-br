---
description: 'Saiba mais sobre o método: ISymUnmanagedVariable:: GetAddressField2'
title: Método ISymUnmanagedVariable::GetAddressField2
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetAddressField2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetAddressField2
helpviewer_keywords:
- GetAddressField2 method [.NET Framework debugging]
- ISymUnmanagedVariable::GetAddressField2 method [.NET Framework debugging]
ms.assetid: 1f25b294-72b6-4882-a49b-6c9d364b6008
topic_type:
- apiref
ms.openlocfilehash: 5d9bc226bfc462157e66b1d8fb43762945cdc016
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762962"
---
# <a name="isymunmanagedvariablegetaddressfield2-method"></a>Método ISymUnmanagedVariable::GetAddressField2

Obtém o segundo campo de endereço para essa variável. Seu significado depende do tipo de endereço.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetAddressField2(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRetVal`  
 fora Um ponteiro para um `ULONG32` que recebe o segundo campo de endereço.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedVariable](isymunmanagedvariable-interface.md)
- [Método GetAddressField1](isymunmanagedvariable-getaddressfield1-method.md)
- [Método GetAddressField3](isymunmanagedvariable-getaddressfield3-method.md)
- [Método GetAddressKind](isymunmanagedvariable-getaddresskind-method.md)
