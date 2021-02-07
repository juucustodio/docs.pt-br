---
description: 'Saiba mais sobre o método: ISymENCUnmanagedMethod:: GetSourceExtentInDocument'
title: Método ISymENCUnmanagedMethod::GetSourceExtentInDocument
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetSourceExtentInDocument
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetSourceExtentInDocument
helpviewer_keywords:
- GetSourceExtentInDocument method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetSourceExtentInDocument method [.NET Framework debugging]
ms.assetid: 9c5566ab-4ec7-4b61-9753-839bb90ae78c
topic_type:
- apiref
ms.openlocfilehash: 6fa9edb524a59b4420ebc737eb8d34eaf0c5c873
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737877"
---
# <a name="isymencunmanagedmethodgetsourceextentindocument-method"></a>Método ISymENCUnmanagedMethod::GetSourceExtentInDocument

Obtém a menor linha inicial e a linha final maior para o método em um documento específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSourceExtentInDocument(  
    [in]  ISymUnmanagedDocument *document,  
    [out] ULONG32* pstartLine,  
    [out] ULONG32* pendLine);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `document`  
 no Um ponteiro para o documento.  
  
 `pstartLine`  
 fora Um ponteiro para um `ULONG32` que recebe a linha inicial.  
  
 `pendLine`  
 fora Um ponteiro para um `ULONG32` que recebe a linha final.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymENCUnmanagedMethod](isymencunmanagedmethod-interface.md)
