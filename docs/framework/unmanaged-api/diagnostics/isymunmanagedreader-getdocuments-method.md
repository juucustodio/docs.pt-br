---
description: 'Saiba mais sobre o método: ISymUnmanagedReader:: getdocumentations'
title: Método ISymUnmanagedReader::GetDocuments
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetDocuments
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetDocuments
helpviewer_keywords:
- GetDocuments method [.NET Framework debugging]
- ISymUnmanagedReader::GetDocuments method [.NET Framework debugging]
ms.assetid: e3b73a3f-d089-4101-a9a9-5e0765d05b61
topic_type:
- apiref
ms.openlocfilehash: 8ee2a2d8e83fcbe2f5b39960fa99e11de2ab4cd2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800208"
---
# <a name="isymunmanagedreadergetdocuments-method"></a>Método ISymUnmanagedReader::GetDocuments

Retorna uma matriz de todos os documentos definidos no repositório de símbolos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDocuments (  
    [in]  ULONG32  cDocs,  
    [out] ULONG32  *pcDocs,  
    [out, size_is (cDocs),  
        length_is (*pcDocs)] ISymUnmanagedDocument *pDocs[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cDocs`  
 no O tamanho da `pDocs` matriz.  
  
 `pcDocs`  
 fora Um ponteiro para uma variável que recebe o comprimento da matriz.  
  
 `pDocs`  
 fora Um ponteiro para uma variável que recebe a matriz de documentos.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedReader](isymunmanagedreader-interface.md)
