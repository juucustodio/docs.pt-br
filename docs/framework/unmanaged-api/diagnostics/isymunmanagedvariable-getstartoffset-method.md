---
description: 'Saiba mais sobre o método: ISymUnmanagedVariable:: GetStartOffset'
title: Método ISymUnmanagedVariable::GetStartOffset
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetStartOffset
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetStartOffset
helpviewer_keywords:
- GetStartOffset method, ISymUnmanagedVariable interface [.NET Framework debugging]
- ISymUnmanagedVariable::GetStartOffset method [.NET Framework debugging]
ms.assetid: 63021fc1-9c2d-4788-811f-fe8ca077206a
topic_type:
- apiref
ms.openlocfilehash: 96ff27cfaf53c7a63c819b1a423e62478cf74832
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762715"
---
# <a name="isymunmanagedvariablegetstartoffset-method"></a>Método ISymUnmanagedVariable::GetStartOffset

Obtém o deslocamento inicial dessa variável dentro de seu pai. Se essa for uma variável local dentro de um escopo, o deslocamento de início se enquadrará dentro dos deslocamentos definidos para o escopo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetStartOffset(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRetVal`  
 fora Um ponteiro para um `ULONG32` que recebe o deslocamento de início.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedVariable](isymunmanagedvariable-interface.md)
- [Método GetEndOffset](isymunmanagedvariable-getendoffset-method.md)
