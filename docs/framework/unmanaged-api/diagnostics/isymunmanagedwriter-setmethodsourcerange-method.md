---
description: 'Saiba mais sobre o método: ISymUnmanagedWriter:: SetMethodSourceRange'
title: Método ISymUnmanagedWriter::SetMethodSourceRange
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.SetMethodSourceRange
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::SetMethodSourceRange
helpviewer_keywords:
- SetMethodSourceRange method [.NET Framework debugging]
- ISymUnmanagedWriter::SetMethodSourceRange method [.NET Framework debugging]
ms.assetid: c698b86e-ace7-4b21-9549-f52d6a034959
topic_type:
- apiref
ms.openlocfilehash: 2e2f0f664d8be30a8c3628100fafb3740d34f54f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762065"
---
# <a name="isymunmanagedwritersetmethodsourcerange-method"></a>Método ISymUnmanagedWriter::SetMethodSourceRange

Especifica os verdadeiros início e término de um método de dentro de um arquivo de origem. Use esse método para especificar a extensão de um método independentemente dos pontos de sequência que existem dentro do método.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetMethodSourceRange(  
    [in] ISymUnmanagedDocumentWriter  *startDoc,  
    [in] ULONG32                      startLine,  
    [in] ULONG32                      startColumn,  
    [in] ISymUnmanagedDocumentWriter  *endDoc,  
    [in] ULONG32                      endLine,  
    [in] ULONG32                      endColumn);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `startDoc`  
 no Um ponteiro para o documento que contém a posição inicial.  
  
 `startLine`  
 no O número da linha inicial.  
  
 `startColumn`  
 no A coluna inicial.  
  
 `endDoc`  
 no Um ponteiro para o documento que contém a posição final.  
  
 `endLine`  
 no O número da linha final.  
  
 `endColumn`  
 no O número da coluna final.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
