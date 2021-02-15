---
description: 'Saiba mais sobre: ISymUnmanagedDocumentWriter:: setverificate Method'
title: Método ISymUnmanagedDocumentWriter::SetCheckSum
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocumentWriter.SetCheckSum
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocumentWriter::SetCheckSum
helpviewer_keywords:
- ISymUnmanagedDocumentWriter::SetCheckSum method [.NET Framework debugging]
- SetCheckSum method [.NET Framework debugging]
ms.assetid: c7e99879-421f-43ce-b193-34733cf30085
topic_type:
- apiref
ms.openlocfilehash: ac2ba9654f3610dca333cf0e06c20696cf31bd1f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710082"
---
# <a name="isymunmanageddocumentwritersetchecksum-method"></a>Método ISymUnmanagedDocumentWriter::SetCheckSum

Define informações de soma de verificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetCheckSum(  
    [in]  GUID     algorithmId,  
    [in]  ULONG32  checkSumSize,  
    [in, size_is(checkSumSize)]  BYTE checkSum[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `algorithmId`  
 no O GUID que representa o identificador do algoritmo.  
  
 `checkSumSize`  
 no Um `ULONG32` que indica o tamanho, em bytes, do `checkSum` buffer.  
  
 `checkSum`  
 no O buffer que armazena as informações de soma de verificação.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedDocumentWriter](isymunmanageddocumentwriter-interface.md)
