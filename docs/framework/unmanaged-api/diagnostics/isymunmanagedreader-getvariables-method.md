---
description: 'Saiba mais sobre o método: ISymUnmanagedReader:: getvariations'
title: Método ISymUnmanagedReader::GetVariables
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetVariables
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetVariables
helpviewer_keywords:
- ISymUnmanagedReader::GetVariables method [.NET Framework debugging]
- GetVariables method, ISymUnmanagedReader interface [.NET Framework debugging]
ms.assetid: 16dc49cb-2c60-4ac8-9c35-020e9afba3f8
topic_type:
- apiref
ms.openlocfilehash: 93208e6c5c65c4c770c533b7ea72de513451d97d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763898"
---
# <a name="isymunmanagedreadergetvariables-method"></a>Método ISymUnmanagedReader::GetVariables

Retorna uma variável não local, dado seu pai e nome.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetVariables (  
    [in]  mdToken  parent,  
    [in]  ULONG32  cVars,  
    [out] ULONG32  *pcVars,  
    [out, size_is (cVars),  
        length_is (*pcVars)] ISymUnmanagedVariable *pVars[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `parent`  
 no O pai da variável.  
  
 `cVars`  
 no O tamanho da `pVars` matriz.  
  
 `pcVars`  
 fora Um ponteiro para a variável que recebe o número de variáveis retornadas em `pVars` .  
  
 `pVars`  
 fora Um ponteiro para a variável que recebe as variáveis.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedReader](isymunmanagedreader-interface.md)
