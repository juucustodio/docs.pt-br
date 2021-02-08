---
description: 'Saiba mais sobre o método: ISymUnmanagedDocument:: GetSourceRange'
title: Método ISymUnmanagedDocument::GetSourceRange
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.GetSourceRange
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::GetSourceRange
helpviewer_keywords:
- ISymUnmanagedDocument::GetSourceRange method [.NET Framework debugging]
- GetSourceRange method [.NET Framework debugging]
ms.assetid: 20fefee7-1040-41ba-93dc-bd42f68b90c2
topic_type:
- apiref
ms.openlocfilehash: 98718298d7bf2f44d418a40f17ad19cdee0b6771
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790159"
---
# <a name="isymunmanageddocumentgetsourcerange-method"></a>Método ISymUnmanagedDocument::GetSourceRange

Retorna o intervalo especificado da fonte inserida para o buffer fornecido. O buffer deve ser grande o suficiente para manter a origem.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSourceRange(  
    [in]  ULONG32  startLine,  
    [in]  ULONG32  startColumn,  
    [in]  ULONG32  endLine,  
    [in]  ULONG32  endColumn,  
    [in]  ULONG32  cSourceBytes,  
    [out] ULONG32  *pcSourceBytes,  
    [out, size_is(cSourceBytes),  
        length_is(*pcSourceBytes)] BYTE source[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `startLine`  
 no A linha inicial no documento atual.  
  
 `startColumn`  
 no A coluna inicial no documento atual.  
  
 `endLine`  
 no A linha final do documento atual.  
  
 `endColumn`  
 no A coluna final no documento atual.  
  
 `cSourceBytes`  
 no O tamanho da origem, em bytes.  
  
 `pcSourceBytes`  
 fora Um ponteiro para uma variável que recebe o tamanho da origem.  
  
 `source`  
 fora O tamanho e o comprimento do intervalo especificado do documento de origem, em bytes.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso.  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedDocument](isymunmanageddocument-interface.md)
