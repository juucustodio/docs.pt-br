---
description: 'Saiba mais sobre o método: ISymUnmanagedScope:: GetChildren'
title: Método ISymUnmanagedScope::GetChildren
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope.GetChildren
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope::GetChildren
helpviewer_keywords:
- ISymUnmanagedScope::GetChildren method [.NET Framework debugging]
- GetChildren method [.NET Framework debugging]
ms.assetid: 0bed524e-cc48-4bf0-b9fa-25d665e63ddb
topic_type:
- apiref
ms.openlocfilehash: 55d72c98d34fcb30a479611895228fbc1b9f7f55
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763495"
---
# <a name="isymunmanagedscopegetchildren-method"></a>Método ISymUnmanagedScope::GetChildren

Obtém os filhos deste escopo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetChildren(  
    [in]  ULONG32  cChildren,  
    [out] ULONG32  *pcChildren,  
    [out, size_is(cChildren),  
        length_is(*pcChildren)] ISymUnmanagedScope* children[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cChildren`  
 no Um `ULONG32` que indica o tamanho da `children` matriz.  
  
 `pcChildren`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho do buffer necessário para conter os filhos.  
  
 `children`  
 fora A matriz de filhos retornada.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedScope](isymunmanagedscope-interface.md)
- [Método GetParent](isymunmanagedscope-getparent-method.md)
