---
description: 'Saiba mais sobre o método: ISymUnmanagedWriter:: OpenMethod'
title: Método ISymUnmanagedWriter::OpenMethod
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.OpenMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::OpenMethod
helpviewer_keywords:
- ISymUnmanagedWriter::OpenMethod method [.NET Framework debugging]
- OpenMethod method [.NET Framework debugging]
ms.assetid: fb90cb7f-af88-45e8-a99f-80a0bbddb08b
topic_type:
- apiref
ms.openlocfilehash: 2cf7e6bf7c632449c25a2b49c7658fa7b1cc287e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762221"
---
# <a name="isymunmanagedwriteropenmethod-method"></a>Método ISymUnmanagedWriter::OpenMethod

Abre um método no qual as informações de símbolo são emitidas. O método fornecido torna-se o método atual para chamadas para definir pontos de sequência, parâmetros e escopos léxicos. Há um escopo lexical implícito em todo o método. Reabrir um método que foi fechado anteriormente apaga todos os símbolos definidos anteriormente para esse método. Pode haver apenas um método Open por vez.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT OpenMethod(  
    [in] mdMethodDef method);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `method`  
 no O token de metadados para o método a ser aberto.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
- [Método CloseMethod](isymunmanagedwriter-closemethod-method.md)
- [Método OpenMethod2](isymunmanagedwriter3-openmethod2-method.md)
