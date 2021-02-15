---
description: 'Saiba mais sobre o método: ISymUnmanagedDocument:: GetCheckSumAlgorithmId'
title: Método ISymUnmanagedDocument::GetCheckSumAlgorithmId
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.GetCheckSumAlgorithmId
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::GetCheckSumAlgorithmId
helpviewer_keywords:
- ISymUnmanagedDocument::GetCheckSumAlgorithmId method [.NET Framework debugging]
- GetCheckSumAlgorithmId method [.NET Framework debugging]
ms.assetid: c7f941cd-e25b-4b85-b1ce-5f77c9208fa9
topic_type:
- apiref
ms.openlocfilehash: 835f56875a1adc3a3b6617a5a0b280f60f918236
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772114"
---
# <a name="isymunmanageddocumentgetchecksumalgorithmid-method"></a>Método ISymUnmanagedDocument::GetCheckSumAlgorithmId

Obtém o identificador de algoritmo de soma de verificação ou retorna um GUID de todos os zeros se não houver nenhuma soma de verificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCheckSumAlgorithmId(  
    [out, retval] GUID*  pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRetVal`  
 fora Um ponteiro para uma variável que recebe o identificador de algoritmo de soma de verificação.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso.  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedDocument](isymunmanageddocument-interface.md)
