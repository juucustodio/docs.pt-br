---
title: Método ISymUnmanagedReader::GetDocumentVersion
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetDocumentVersion
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetDocumentVersion
helpviewer_keywords:
- GetDocumentVersion method [.NET Framework debugging]
- ISymUnmanagedReader::GetDocumentVersion method [.NET Framework debugging]
ms.assetid: a51f1f64-e084-44c5-830c-2222da5a6bbf
topic_type:
- apiref
ms.openlocfilehash: c2cc541b2a78f16d5ca6b19405794faa825a9d72
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615027"
---
# <a name="isymunmanagedreadergetdocumentversion-method"></a>Método ISymUnmanagedReader::GetDocumentVersion
Obtém a versão especificada do documento especificado. A versão do documento começa em 1 e é incrementada toda vez que o documento é atualizado usando o método [UpdateSymbolStore](isymunmanagedreader-updatesymbolstore-method.md) . Se o `pbCurrent` parâmetro for `true` , esta é a versão mais recente do documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDocumentVersion (  
    [in]  ISymUnmanagedDocument *pDoc,  
    [out] int* version,  
    [out] BOOL* pbCurrent);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `pDoc`  
 no O documento especificado.  
  
 `version`  
 fora Um ponteiro para uma variável que recebe a versão do documento especificado.  
  
 `pbCurrent`  
 fora Um ponteiro para uma variável que recebe `true` se esta é a versão mais recente do documento ou `false` se não é a versão mais recente.  
  
## <a name="return-value"></a>Valor retornado  
 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Confira também

- [Interface ISymUnmanagedReader](isymunmanagedreader-interface.md)
