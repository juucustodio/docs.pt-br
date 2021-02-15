---
description: 'Saiba mais sobre o método: ISymUnmanagedWriter:: UsingNamespace'
title: Método ISymUnmanagedWriter::UsingNamespace
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.UsingNamespace
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::UsingNamespace
helpviewer_keywords:
- UsingNamespace method [.NET Framework debugging]
- ISymUnmanagedWriter::UsingNamespace method [.NET Framework debugging]
ms.assetid: 8d746e0a-d158-4983-88da-db0a0856bc0b
topic_type:
- apiref
ms.openlocfilehash: e7d56cded125aac6154d4315c587f58f946a9a82
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761948"
---
# <a name="isymunmanagedwriterusingnamespace-method"></a>Método ISymUnmanagedWriter::UsingNamespace

Especifica que o nome de namespace totalmente qualificado fornecido está sendo usado dentro do escopo léxico aberto no momento. O namespace será usado em todos os escopos que herdam do escopo aberto no momento. Fechar o escopo atual também irá parar o uso do namespace.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT UsingNamespace(  
    [in] const WCHAR *fullName);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fullName`  
 no Um ponteiro para o nome totalmente qualificado do namespace.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
