---
description: 'Saiba mais sobre o método: ISymENCUnmanagedMethod:: GetFileNameFromOffset'
title: Método ISymENCUnmanagedMethod::GetFileNameFromOffset
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetFileNameFromOffset
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetFileNameFromOffset
helpviewer_keywords:
- GetFileNameFromOffset method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetFileNameFromOffset method [.NET Framework debugging]
ms.assetid: 00e2e194-12f5-436e-a997-2b9d3e844d4f
topic_type:
- apiref
ms.openlocfilehash: 1322e55f115958a2f4b2634dfa25eff127167d54
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737994"
---
# <a name="isymencunmanagedmethodgetfilenamefromoffset-method"></a>Método ISymENCUnmanagedMethod::GetFileNameFromOffset

Obtém o nome do arquivo da linha associada a um deslocamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFileNameFromOffset(  
    [in]  ULONG32  dwOffset,  
    [in]  ULONG32  cchName,  
    [out] ULONG32  *pcchName,  
    [out, size_is(cchName),  
       length_is(*pcchName)] WCHAR szName[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwOffset`  
 no Um `ULONG32` que contém o deslocamento.  
  
 `cchName`  
 no Um `ULONG32` que indica o tamanho do `szName` buffer.  
  
 `pcchName`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em caracteres, do buffer necessário para conter os nomes de arquivo.  
  
 `szName`  
 fora O buffer que contém os nomes de arquivo.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymENCUnmanagedMethod](isymencunmanagedmethod-interface.md)
