---
description: 'Saiba mais sobre: método ISymUnmanagedScope2:: getconstantes'
title: Método ISymUnmanagedScope2::GetConstants
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope2.GetConstants
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope2::GetConstants
helpviewer_keywords:
- ISymUnmanagedScope2::GetConstants method [.NET Framework debugging]
- GetConstants method [.NET Framework debugging]
ms.assetid: f241b620-9ec5-42fd-92ef-3b22329db72a
topic_type:
- apiref
ms.openlocfilehash: 025bb9ddd0501f2309b2c0a3f7af20eb961604cb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763209"
---
# <a name="isymunmanagedscope2getconstants-method"></a>Método ISymUnmanagedScope2::GetConstants

Obtém as constantes locais definidas neste escopo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetConstants(  
     [in]  ULONG32  cConstants,  
     [out] ULONG32  *pcConstants,  
     [out, size_is(cConstants),  
         length_is(*pcConstants)] ISymUnmanagedConstant*
             constants[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cConstants`  
 no O comprimento do buffer para o qual o `pcConstants` parâmetro aponta.  
  
 `pcConstants`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em caracteres, do buffer necessário para conter as constantes.  
  
 `constants`  
 fora O buffer que armazena as constantes.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedScope2](isymunmanagedscope2-interface.md)
