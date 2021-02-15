---
description: 'Saiba mais sobre o método: ISymUnmanagedSymbolSearchInfo:: GetSearchPath'
title: Método ISymUnmanagedSymbolSearchInfo::GetSearchPath
ms.date: 03/30/2017
api_name:
- ISymUnmanagedSymbolSearchInfo.GetSearchPath
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedSymbolSearchInfo::GetSearchPath
helpviewer_keywords:
- GetSearchPath method [.NET Framework debugging]
- ISymUnmanagedSymbolSearchInfo::GetSearchPath method [.NET Framework debugging]
ms.assetid: b588d470-53c2-4492-be8c-957323eaca0b
topic_type:
- apiref
ms.openlocfilehash: 2ae85733ccca8ac63fbca5d2556026221e5681bb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763027"
---
# <a name="isymunmanagedsymbolsearchinfogetsearchpath-method"></a>Método ISymUnmanagedSymbolSearchInfo::GetSearchPath

Obtém o caminho de pesquisa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSearchPathLength(  
    [out] ULONG32 *pcchPath);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pcchPath`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em caracteres, do buffer necessário para conter o caminho de pesquisa.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedSymbolSearchInfo](isymunmanagedsymbolsearchinfo-interface.md)
