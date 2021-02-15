---
description: 'Saiba mais sobre o método: ISymUnmanagedWriter:: Close'
title: Método ISymUnmanagedWriter::Close
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.Close
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::Close
helpviewer_keywords:
- Close method, ISymUnmanagedWriter interface [.NET Framework debugging]
- ISymUnmanagedWriter::Close method [.NET Framework debugging]
ms.assetid: 4cce59e1-80b9-4fc4-b3aa-126f1c5876bc
topic_type:
- apiref
ms.openlocfilehash: 02f4d8d4a232240160ad5065947282f40af42f4e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762624"
---
# <a name="isymunmanagedwriterclose-method"></a>Método ISymUnmanagedWriter::Close

Fecha o gravador de símbolo depois de confirmar os símbolos para o repositório de símbolos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Close();  
```  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="remarks"></a>Comentários  

 Após essa chamada, o gravador de símbolo se torna inválido para atualizações adicionais. Para fechar o gravador de símbolo sem confirmar os símbolos, use o método [ISymUnmanagedWriter:: Abort](isymunmanagedwriter-abort-method.md) em vez disso.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
