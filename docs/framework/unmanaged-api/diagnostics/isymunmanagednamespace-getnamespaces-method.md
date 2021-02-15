---
description: 'Saiba mais sobre o método: ISymUnmanagedNamespace:: getnamespaces'
title: Método ISymUnmanagedNamespace::GetNamespaces
ms.date: 03/30/2017
api_name:
- ISymUnmanagedNamespace.GetNamespaces
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedNamespace::GetNamespaces
helpviewer_keywords:
- ISymUnmanagedNamespace::GetNamespaces method [.NET Framework debugging]
- GetNamespaces method, ISymUnmanagedNamespace interface [.NET Framework debugging]
ms.assetid: 0ea9d9af-8709-4a46-872b-f54d9e840088
topic_type:
- apiref
ms.openlocfilehash: f17b16e2a3a7001d16c86dd6dc95241c1b0785e6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709900"
---
# <a name="isymunmanagednamespacegetnamespaces-method"></a>Método ISymUnmanagedNamespace::GetNamespaces

Obtém os filhos deste namespace.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetNamespaces(  
    [in]  ULONG32  cNameSpaces,  
    [out] ULONG32  *pcNameSpaces,  
    [out, size_is(cNameSpaces), length_is(*pcNameSpaces)]  
        ISymUnmanagedNamespace* namespaces[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cNameSpaces`  
 no Um `ULONG32` que indica o tamanho da `namespaces` matriz.  
  
 `pcNameSpaces`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em caracteres, do buffer necessário para conter os namespaces.  
  
 `namespaces`  
 fora Um ponteiro para o buffer que contém os namespaces.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedNamespace](isymunmanagednamespace-interface.md)
