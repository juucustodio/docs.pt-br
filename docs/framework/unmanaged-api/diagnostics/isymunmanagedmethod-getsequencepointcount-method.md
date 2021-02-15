---
description: 'Saiba mais sobre o método: ISymUnmanagedMethod:: GetSequencePointCount'
title: Método ISymUnmanagedMethod::GetSequencePointCount
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetSequencePointCount
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetSequencePointCount
helpviewer_keywords:
- ISymUnmanagedMethod::GetSequencePointCount method [.NET Framework debugging]
- GetSequencePointCount method [.NET Framework debugging]
ms.assetid: 836133e8-6108-4b9b-b0a9-bce4e08dccda
topic_type:
- apiref
ms.openlocfilehash: 6e0341ddc151454de8764a47a92556ab1925bfa1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709992"
---
# <a name="isymunmanagedmethodgetsequencepointcount-method"></a>Método ISymUnmanagedMethod::GetSequencePointCount

Obtém a contagem de pontos de sequência dentro deste método.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSequencePointCount(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRetVal`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho do buffer necessário para conter os pontos de sequência.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedMethod](isymunmanagedmethod-interface.md)
