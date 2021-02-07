---
description: 'Saiba mais sobre o método: ISymUnmanagedMethod:: GetSourceStartEnd'
title: Método ISymUnmanagedMethod::GetSourceStartEnd
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetSourceStartEnd
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetSourceStartEnd
helpviewer_keywords:
- GetSourceStartEnd method [.NET Framework debugging]
- ISymUnmanagedMethod::GetSourceStartEnd method [.NET Framework debugging]
ms.assetid: 2a420900-01f1-4461-8777-3a34a6dc1426
topic_type:
- apiref
ms.openlocfilehash: 0d247427998970d86c1ad1ec37f5b32a846a6f7c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709978"
---
# <a name="isymunmanagedmethodgetsourcestartend-method"></a>Método ISymUnmanagedMethod::GetSourceStartEnd

Obtém as posições do documento inicial e final da origem deste método. A primeira posição da matriz é o início e a segunda posição da matriz é o final.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSourceStartEnd(  
    [in]  ISymUnmanagedDocument  *docs[2],  
    [in]  ULONG32                lines[2],  
    [in]  ULONG32                columns[2],  
    [out] BOOL                   *pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `docs`  
 no Os documentos de origem inicial e final.  
  
 `lines`  
 no As linhas inicial e final nos documentos de origem correspondentes.  
  
 `columns`  
 no As colunas inicial e final nos documentos de origem correspondentes.  
  
 `pRetVal`  
 [fora] `true` Se as posições foram definidas; caso contrário, `false` .  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedMethod](isymunmanagedmethod-interface.md)
