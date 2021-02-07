---
description: 'Saiba mais sobre o método: ISymUnmanagedReader:: GetMethodFromDocumentPosition'
title: Método ISymUnmanagedReader::GetMethodFromDocumentPosition
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetMethodFromDocumentPosition
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetMethodFromDocumentPosition
helpviewer_keywords:
- GetMethodFromDocumentPosition method [.NET Framework debugging]
- ISymUnmanagedReader::GetMethodFromDocumentPosition method [.NET Framework debugging]
ms.assetid: 55773dbc-9053-46e3-8a3c-86caa9d91fb4
topic_type:
- apiref
ms.openlocfilehash: 1289b02f8ea8440dcd1b308b6c91a46a213cabb2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764080"
---
# <a name="isymunmanagedreadergetmethodfromdocumentposition-method"></a>Método ISymUnmanagedReader::GetMethodFromDocumentPosition

Retorna o método que contém o ponto de interrupção na posição especificada em um documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMethodFromDocumentPosition (  
    [in]  ISymUnmanagedDocument*  document,  
    [in]  ULONG32  line,  
    [in]  ULONG32  column,  
    [out, retval] ISymUnmanagedMethod**  pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `document`  
 no O documento especificado.  
  
 `line`  
 no A linha do documento especificado.  
  
 `column`  
 no A coluna do documento especificado.  
  
 `pRetVal`  
 fora Um ponteiro para o endereço de um objeto de [interface ISymUnmanagedMethod](isymunmanagedmethod-interface.md) que representa o método que contém o ponto de interrupção.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedReader](isymunmanagedreader-interface.md)
