---
description: 'Saiba mais sobre o método: ISymUnmanagedDocument:: GetLanguage'
title: Método ISymUnmanagedDocument::GetLanguage
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.GetLanguage
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::GetLanguage
helpviewer_keywords:
- ISymUnmanagedDocument::GetLanguage method [.NET Framework debugging]
- GetLanguage method [.NET Framework debugging]
ms.assetid: c6639418-e9f2-4a99-8ce2-ec9876e0bc79
topic_type:
- apiref
ms.openlocfilehash: f30636303d310ed91aa4229f52a3197a29190d3a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710303"
---
# <a name="isymunmanageddocumentgetlanguage-method"></a>Método ISymUnmanagedDocument::GetLanguage

Obtém o identificador de idioma deste documento  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLanguage(  
    [out, retval]  GUID*  pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRetVal`  
 fora Um ponteiro para uma variável que recebe o identificador de idioma.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso.  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedDocument](isymunmanageddocument-interface.md)
