---
description: 'Saiba mais sobre o método: ISymUnmanagedVariable:: GetName'
title: Método ISymUnmanagedVariable::GetName
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetName
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetName
helpviewer_keywords:
- GetName method, ISymUnmanagedVariable interface [.NET Framework debugging]
- ISymUnmanagedVariable::GetName method [.NET Framework debugging]
ms.assetid: eedf1ef0-9d4a-4847-a201-4e99572dfe5e
topic_type:
- apiref
ms.openlocfilehash: 88d8cf4c81200a30e2a102b63af2817fef2b50c9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762780"
---
# <a name="isymunmanagedvariablegetname-method"></a>Método ISymUnmanagedVariable::GetName

Obtém o nome dessa variável.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetName(  
    [in]  ULONG32  cchName,  
    [out] ULONG32  *pcchName,  
    [out, size_is(cchName),  
        length_is(*pcchName)] WCHAR szName[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cchName`  
 no O comprimento do buffer para o qual o `pcchName` parâmetro aponta.  
  
 `pcchName`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em caracteres, do buffer necessário para conter o nome, incluindo a terminação nula.  
  
 `szName`  
 fora O buffer que armazena o nome.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedVariable](isymunmanagedvariable-interface.md)
