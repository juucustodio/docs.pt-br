---
description: 'Saiba mais sobre o método: ISymUnmanagedReader:: GetMethodByVersion'
title: Método ISymUnmanagedReader::GetMethodByVersion
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetMethodByVersion
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetMethodByVersion
helpviewer_keywords:
- ISymUnmanagedReader::GetMethodByVersion method [.NET Framework debugging]
- GetMethodByVersion method [.NET Framework debugging]
ms.assetid: 6ddb0631-4569-41b3-93e4-50fdfaa486dc
topic_type:
- apiref
ms.openlocfilehash: 6b2fa3ff3af91d59bb79029d039e5656610bebff
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772062"
---
# <a name="isymunmanagedreadergetmethodbyversion-method"></a>Método ISymUnmanagedReader::GetMethodByVersion

Obtém um método de leitor de símbolo, dado um token de método e um número de versão de edição e cópia. Os números de versão começam em 1 e são incrementados cada vez que o método é alterado como resultado de uma operação de edição e cópia.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMethodByVersion (  
    [in]  mdMethodDef  token,  
    [in]  int  version,  
    [out, retval] ISymUnmanagedMethod** pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `token`  
 no O token do método.  
  
 `version`  
 no A versão do método.  
  
 `pRetVal`  
 fora Um ponteiro para a interface retornada.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedReader](isymunmanagedreader-interface.md)
