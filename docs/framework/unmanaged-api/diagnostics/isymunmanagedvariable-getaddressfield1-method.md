---
description: 'Saiba mais sobre o método: ISymUnmanagedVariable:: GetAddressField1'
title: Método ISymUnmanagedVariable::GetAddressField1
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetAddressField1
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetAddressField1
helpviewer_keywords:
- GetAddressField1 method [.NET Framework debugging]
- ISymUnmanagedVariable::GetAddressField1 method [.NET Framework debugging]
ms.assetid: 25788ed1-0ce3-4b97-96fc-88f8997812a3
topic_type:
- apiref
ms.openlocfilehash: 1ff6862cef52ef8fcb449563198c2df1de356530
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762988"
---
# <a name="isymunmanagedvariablegetaddressfield1-method"></a>Método ISymUnmanagedVariable::GetAddressField1

Obtém o primeiro campo de endereço para essa variável. Seu significado depende do tipo de endereço.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetAddressField1(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRetVal`  
 fora Um ponteiro para um `ULONG32` que recebe o primeiro campo de endereço.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedVariable](isymunmanagedvariable-interface.md)
- [Método GetAddressField2](isymunmanagedvariable-getaddressfield2-method.md)
- [Método GetAddressField3](isymunmanagedvariable-getaddressfield3-method.md)
- [Método GetAddressKind](isymunmanagedvariable-getaddresskind-method.md)
