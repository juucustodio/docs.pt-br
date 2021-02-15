---
description: 'Saiba mais sobre o método: ISymUnmanagedNamespace:: getvariations'
title: Método ISymUnmanagedNamespace::GetVariables
ms.date: 03/30/2017
api_name:
- ISymUnmanagedNamespace.GetVariables
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedNamespace::GetVariables
helpviewer_keywords:
- ISymUnmanagedNamespace::GetVariables method [.NET Framework debugging]
- GetVariables method, ISymUnmanagedNamespace interface [.NET Framework debugging]
ms.assetid: ea7c1617-f3ce-4220-8288-f2b50eaf0f0f
topic_type:
- apiref
ms.openlocfilehash: 63316bf3ba1e4736d542be3362076c3ae6e95def
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99721197"
---
# <a name="isymunmanagednamespacegetvariables-method"></a>Método ISymUnmanagedNamespace::GetVariables

Retorna todas as variáveis definidas no escopo global dentro deste namespace.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetVariables(  
    [in]  ULONG32  cVars,  
    [out] ULONG32  *pcVars,  
    [out, size_is(cVars), length_is(*pcVars)]  
        ISymUnmanagedVariable *pVars[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cVars`  
 no Um `ULONG32` que indica o tamanho da `pVars` matriz.  
  
 `pcVars`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho do buffer necessário para conter os namespaces.  
  
 `pVars`  
 fora Um ponteiro para um buffer que contém os namespaces.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedNamespace](isymunmanagednamespace-interface.md)
