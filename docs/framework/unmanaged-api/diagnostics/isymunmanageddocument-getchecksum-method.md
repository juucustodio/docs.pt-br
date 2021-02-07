---
description: 'Saiba mais sobre: ISymUnmanagedDocument:: método getchecksum'
title: Método ISymUnmanagedDocument::GetCheckSum
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.GetCheckSum
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::GetCheckSum
helpviewer_keywords:
- ISymUnmanagedDocument::GetCheckSum method [.NET Framework debugging]
- GetCheckSum method [.NET Framework debugging]
ms.assetid: 9bc881b3-e2ce-48a7-ad69-17eaaa304120
topic_type:
- apiref
ms.openlocfilehash: 9f9a42e58b22661a2233fcb457b9b42b0d6a3d1a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737682"
---
# <a name="isymunmanageddocumentgetchecksum-method"></a>Método ISymUnmanagedDocument::GetCheckSum

Obtém a soma de verificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCheckSum(  
    [in]  ULONG32  cData,  
    [out] ULONG32  *pcData,  
    [out, size_is(cData), length_is(*pcData)] BYTE data[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cData`  
 no O comprimento do buffer fornecido pelo `data` parâmetro  
  
 `pcData`  
 fora O tamanho e o comprimento da soma de verificação, em bytes.  
  
 `data`  
 fora O buffer que recebe a soma de verificação.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, um código de erro.  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedDocument](isymunmanageddocument-interface.md)
