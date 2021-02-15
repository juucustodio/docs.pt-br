---
description: 'Saiba mais sobre o método: ISymUnmanagedENCUpdate:: GetLocalVariables'
title: Método ISymUnmanagedENCUpdate::GetLocalVariables
ms.date: 03/30/2017
api_name:
- ISymUnmanagedENCUpdate.GetLocalVariables
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedENCUpdate::GetLocalVariables
helpviewer_keywords:
- ISymUnmanagedENCUpdate::GetLocalVariables method [.NET Framework debugging]
- GetLocalVariables method [.NET Framework debugging]
ms.assetid: 5c8840be-ffea-447f-9c8d-178f1eaf8d06
topic_type:
- apiref
ms.openlocfilehash: bc034603dd6a09ea78dad789e11ea951d65e839b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99721457"
---
# <a name="isymunmanagedencupdategetlocalvariables-method"></a>Método ISymUnmanagedENCUpdate::GetLocalVariables

Obtém as variáveis locais.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLocalVariables(  
    [in]  mdMethodDef  mdMethodToken,  
    [in]  ULONG        cLocals,  
    [out, size_is(cLocals), length_is(*pceltFetched)]  
        ISymUnmanagedVariable *rgLocals[],  
    [out] ULONG        *pceltFetched);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `mdMethodToken`  
 no O token de metadados do método.  
  
 `cLocals`  
 no Um `ULONG` que indica o tamanho do `rgLocals` parâmetro.  
  
 `rgLocals`  
 fora A matriz retornada de instâncias de [ISymUnmanagedVariable](isymunmanagedvariable-interface.md) .  
  
 `pceltFetched`  
 fora Um ponteiro para um `ULONG` que recebe o tamanho do `rgLocals` buffer necessário para conter os locais.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedENCUpdate](isymunmanagedencupdate-interface.md)
