---
description: 'Saiba mais sobre o método: ISymUnmanagedScope:: GetMethod'
title: Método ISymUnmanagedScope::GetMethod
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope.GetMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope::GetMethod
helpviewer_keywords:
- GetMethod method, ISymUnmanagedScope interface [.NET Framework debugging]
- ISymUnmanagedScope::GetMethod method [.NET Framework debugging]
ms.assetid: a61866ee-221a-45b9-a1b7-395825b77872
topic_type:
- apiref
ms.openlocfilehash: 7dfc5f41d849d47bfaf600e40a7ccc9dd45da676
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763391"
---
# <a name="isymunmanagedscopegetmethod-method"></a>Método ISymUnmanagedScope::GetMethod

Obtém o método que contém esse escopo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMethod(  
    [out, retval] ISymUnmanagedMethod** pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRetVal`  
 fora Um ponteiro para a interface [ISymUnmanagedMethod](isymunmanagedmethod-interface.md) retornada.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedScope](isymunmanagedscope-interface.md)
