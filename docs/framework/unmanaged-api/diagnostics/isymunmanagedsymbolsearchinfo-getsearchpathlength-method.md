---
description: 'Saiba mais sobre o método: ISymUnmanagedSymbolSearchInfo:: GetSearchPathLength'
title: Método ISymUnmanagedSymbolSearchInfo::GetSearchPathLength
ms.date: 03/30/2017
api_name:
- ISymUnmanagedSymbolSearchInfo.GetSearchPathLength
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedSymbolSearchInfo::GetSearchPathLength
helpviewer_keywords:
- GetSearchPathLength method [.NET Framework debugging]
- ISymUnmanagedSymbolSearchInfo::GetSearchPathLength method [.NET Framework debugging]
ms.assetid: 274e73cf-8333-47ba-ac12-70214e2b0112
topic_type:
- apiref
ms.openlocfilehash: 3d5faf9d972881ff9c1eaf71bcaa6f68da46dae6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763014"
---
# <a name="isymunmanagedsymbolsearchinfogetsearchpathlength-method"></a>Método ISymUnmanagedSymbolSearchInfo::GetSearchPathLength

Obtém o comprimento do caminho de pesquisa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSearchPathLength(  
    [out] ULONG32 *pcchPath);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pcchPath`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em caracteres, do buffer necessário para conter o comprimento do caminho de pesquisa.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedSymbolSearchInfo](isymunmanagedsymbolsearchinfo-interface.md)
