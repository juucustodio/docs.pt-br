---
description: 'Saiba mais sobre: método ISymUnmanagedMethod:: GetToken'
title: Método ISymUnmanagedMethod::GetToken
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetToken
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetToken
helpviewer_keywords:
- ISymUnmanagedMethod::GetToken method [.NET Framework debugging]
- GetToken method, ISymUnmanagedMethod interface [.NET Framework debugging]
ms.assetid: 4effbe95-c36e-4a45-8b2a-ee21339415fb
topic_type:
- apiref
ms.openlocfilehash: fde9936a6e79b9d1fff5b38ee7242cf5bb71369d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99721301"
---
# <a name="isymunmanagedmethodgettoken-method"></a>Método ISymUnmanagedMethod::GetToken

Retorna o token de metadados para esse método.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetToken(  
   [out, retval]  mdMethodDef  *pToken);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pToken`  
 fora Um ponteiro para um `mdMethodDef` que recebe o tamanho, em caracteres, do buffer necessário para conter os metadados.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedMethod](isymunmanagedmethod-interface.md)
