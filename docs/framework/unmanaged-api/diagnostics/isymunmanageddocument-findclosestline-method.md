---
description: 'Saiba mais sobre o método: ISymUnmanagedDocument:: FindClosestLine'
title: Método ISymUnmanagedDocument::FindClosestLine
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.FindClosestLine
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::FindClosestLine
helpviewer_keywords:
- FindClosestLine method [.NET Framework debugging]
- ISymUnmanagedDocument::FindClosestLine method [.NET Framework debugging]
ms.assetid: 628f2a04-e529-407d-841e-3b3da219a9cb
topic_type:
- apiref
ms.openlocfilehash: 0409a5cc29bf148a49a5267d34662f763fc302d9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737825"
---
# <a name="isymunmanageddocumentfindclosestline-method"></a>Método ISymUnmanagedDocument::FindClosestLine

Retorna a linha mais próxima que é um ponto de sequência, dada uma linha neste documento que pode ou não ser um ponto de sequência.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FindClosestLine(  
    [in]  ULONG32  line,  
    [out, retval] ULONG32*  pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `line`  
 no Uma linha neste documento.  
  
 `pRetVal`  
 fora Um ponteiro para uma variável que recebe a linha.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, um código de erro.  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedDocument](isymunmanageddocument-interface.md)
