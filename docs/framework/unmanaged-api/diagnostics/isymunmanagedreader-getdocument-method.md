---
description: 'Saiba mais sobre o método: ISymUnmanagedReader:: GetDocument'
title: Método ISymUnmanagedReader::GetDocument
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetDocument
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetDocument
helpviewer_keywords:
- ISymUnmanagedReader::GetDocument method [.NET Framework debugging]
- GetDocument method [.NET Framework debugging]
ms.assetid: bb203853-6a6d-4027-b9e9-603a7f28b9d3
topic_type:
- apiref
ms.openlocfilehash: 7f2f31467cfd00de68737224a2c1af5b1e78efed
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764093"
---
# <a name="isymunmanagedreadergetdocument-method"></a>Método ISymUnmanagedReader::GetDocument

Localiza um documento. O idioma do documento, o fornecedor e o tipo são opcionais.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDocument (  
    [in]  WCHAR  *url,  
    [in]  GUID   language,  
    [in]  GUID   languageVendor,  
    [in]  GUID   documentType,  
    [out, retval] ISymUnmanagedDocument** pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `url`  
 no A URL que identifica o documento.  
  
 `language`  
 no O idioma do documento. Esse parâmetro é opcional.  
  
 `languageVendor`  
 no A identidade do fornecedor para o idioma do documento. Esse parâmetro é opcional.  
  
 `documentType`  
 no O tipo do documento. Esse parâmetro é opcional.  
  
 `pRetVal`  
 fora Um ponteiro para a interface retornada.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedReader](isymunmanagedreader-interface.md)
