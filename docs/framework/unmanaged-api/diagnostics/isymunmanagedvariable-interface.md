---
description: 'Saiba mais sobre: interface ISymUnmanagedVariable'
title: Interface ISymUnmanagedVariable
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable
helpviewer_keywords:
- ISymUnmanagedVariable interface [.NET Framework debugging]
ms.assetid: 704c69ba-77bc-40d7-8c0c-400061686321
topic_type:
- apiref
ms.openlocfilehash: 15b6c7018f92ad4c82abb9e5b4e52bf428b3f54b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762689"
---
# <a name="isymunmanagedvariable-interface"></a>Interface ISymUnmanagedVariable

Representa uma variável, como um parâmetro, uma variável local ou um campo.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetAddressField1](isymunmanagedvariable-getaddressfield1-method.md)|Obtém o primeiro campo de endereço para essa variável. Seu significado depende do tipo de endereço.|  
|[Método GetAddressField2](isymunmanagedvariable-getaddressfield2-method.md)|Obtém o segundo campo de endereço para essa variável. Seu significado depende do tipo de endereço.|  
|[Método GetAddressField3](isymunmanagedvariable-getaddressfield3-method.md)|Obtém o terceiro campo de endereço para essa variável. Seu significado depende do tipo de endereço.|  
|[Método GetAddressKind](isymunmanagedvariable-getaddresskind-method.md)|Obtém o tipo de endereço dessa variável.|  
|[Método GetAttributes](isymunmanagedvariable-getattributes-method.md)|Obtém os sinalizadores de atributo para essa variável.|  
|[Método GetEndOffset](isymunmanagedvariable-getendoffset-method.md)|Obtém o deslocamento final dessa variável dentro de seu pai.|  
|[Método GetName](isymunmanagedvariable-getname-method.md)|Obtém o nome dessa variável.|  
|[Método GetSignature](isymunmanagedvariable-getsignature-method.md)|Obtém a assinatura dessa variável.|  
|[Método GetStartOffset](isymunmanagedvariable-getstartoffset-method.md)|Obtém o deslocamento inicial dessa variável dentro de seu pai.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
