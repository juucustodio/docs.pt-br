---
description: 'Saiba mais sobre o método: ISymUnmanagedWriter3:: OpenMethod2'
title: Método ISymUnmanagedWriter3::OpenMethod2
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter3.OpenMethod2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter3::OpenMethod2
helpviewer_keywords:
- ISymUnmanagedWriter3::OpenMethod2 method [.NET Framework debugging]
- OpenMethod2 method [.NET Framework debugging]
ms.assetid: 025e358c-448f-4423-a2f2-57acf437c8a5
topic_type:
- apiref
ms.openlocfilehash: 7e76be03598599a6498ed45bc3799c6d6f21e088
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761688"
---
# <a name="isymunmanagedwriter3openmethod2-method"></a>Método ISymUnmanagedWriter3::OpenMethod2

Abre um método e fornece seu deslocamento de seção real na imagem.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT OpenMethod2(
    [in] mdMethodDef method,  
    [in] ULONG32 isect,  
    [in] ULONG32 offset);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `method`  
 no O token de metadados para o método a ser aberto.  
  
 `isect`  
 no O deslocamento da seção na imagem.  
  
 `offset`  
 no O deslocamento na imagem.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter3](isymunmanagedwriter3-interface.md)
- [Método OpenMethod](isymunmanagedwriter-openmethod-method.md)
