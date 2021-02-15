---
description: 'Saiba mais sobre o método: ISymUnmanagedScope:: GetLocals'
title: Método ISymUnmanagedScope::GetLocals
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope.GetLocals
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope::GetLocals
helpviewer_keywords:
- GetLocals method [.NET Framework debugging]
- ISymUnmanagedScope::GetLocals method [.NET Framework debugging]
ms.assetid: 17c45f15-8c44-44da-b070-f902077b36e4
topic_type:
- apiref
ms.openlocfilehash: 6b20d8a79e826be0bd191d46e794f8dad45c4810
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763404"
---
# <a name="isymunmanagedscopegetlocals-method"></a>Método ISymUnmanagedScope::GetLocals

Obtém as variáveis locais definidas nesse escopo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLocals(  
    [in]  ULONG32  cLocals,  
    [out] ULONG32  *pcLocals,  
    [out, size_is(cLocals),  
        length_is(*pcLocals)] ISymUnmanagedVariable* locals[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cLocals`  
 no Um `ULONG32` que indica o tamanho da `locals` matriz.  
  
 `pcLocals`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho do buffer necessário para conter as variáveis locais.  
  
 `locals`  
 fora A matriz que recebe as variáveis locais.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedScope](isymunmanagedscope-interface.md)
