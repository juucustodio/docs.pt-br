---
description: 'Saiba mais sobre o método: ISymUnmanagedMethod:: getranges'
title: Método ISymUnmanagedMethod::GetRanges
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetRanges
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetRanges
helpviewer_keywords:
- ISymUnmanagedMethod::GetRanges method [.NET Framework debugging]
- GetRanges method [.NET Framework debugging]
ms.assetid: a85283d8-379c-417a-9736-ddeeef9bcf50
topic_type:
- apiref
ms.openlocfilehash: e6a1da285c0574ef5910e8e727c3bcc5cb9e5d35
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790094"
---
# <a name="isymunmanagedmethodgetranges-method"></a>Método ISymUnmanagedMethod::GetRanges

Dada uma posição em um documento, retorna uma matriz de pares de deslocamento inicial e final que correspondem aos intervalos da MSIL (Microsoft Intermediate Language) que a posição aborda nesse método. A matriz é uma matriz de inteiros e tem o formato [início, fim, início, fim]. O número de pares de intervalo é o comprimento da matriz dividida por 2.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRanges(  
    [in]  ISymUnmanagedDocument* document,  
    [in]  ULONG32                line,  
    [in]  ULONG32                column,  
    [in]  ULONG32                cRanges,  
    [out] ULONG32                *pcRanges,  
    [out, size_is(cRanges),  
        length_is(*pcRanges)] ULONG32 ranges[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `document`  
 no O documento para o qual o deslocamento é solicitado.  
  
 `line`  
 no A linha do documento correspondente aos intervalos.  
  
 `column`  
 no A coluna de documento correspondente aos intervalos.  
  
 `cRanges`  
 no O tamanho da `ranges` matriz.  
  
 `pcRanges`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho do buffer necessário para conter os intervalos.  
  
 `ranges`  
 fora Um ponteiro para o buffer que recebe os intervalos.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedMethod](isymunmanagedmethod-interface.md)
