---
description: 'Saiba mais sobre o método: ISymENCUnmanagedMethod:: GetDocumentsForMethod'
title: Método ISymENCUnmanagedMethod::GetDocumentsForMethod
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetDocumentsForMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetDocumentsForMethod
helpviewer_keywords:
- GetDocumentsForMethod method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetDocumentsForMethod method [.NET Framework debugging]
ms.assetid: bd6ccde5-d578-48d8-abed-b474fbd48d13
topic_type:
- apiref
ms.openlocfilehash: 01c7280abe437266618d96c6e195e61a4f830131
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99721535"
---
# <a name="isymencunmanagedmethodgetdocumentsformethod-method"></a>Método ISymENCUnmanagedMethod::GetDocumentsForMethod

Obtém os documentos em que este método tem linhas.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDocumentsForMethod(  
    [in]  ULONG32  cDocs,  
    [out] ULONG32  *pcDocs,
    [in, size_is(cDocs)] ISymUnmanagedDocument* documents[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cDocs`  
 no O comprimento do buffer apontado por `pcDocs` .  
  
 `pcDocs`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em caracteres, do buffer necessário para conter os documentos.  
  
 `documents`  
 no O buffer que contém os documentos.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, um código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymENCUnmanagedMethod](isymencunmanagedmethod-interface.md)
