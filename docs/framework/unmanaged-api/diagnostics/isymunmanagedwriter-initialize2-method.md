---
description: 'Saiba mais sobre o método: ISymUnmanagedWriter:: Initialize2'
title: Método ISymUnmanagedWriter::Initialize2
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.Initialize2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::Initialize2
helpviewer_keywords:
- ISymUnmanagedWriter::Initialize2 method [.NET Framework debugging]
- Initialize2 method [.NET Framework debugging]
ms.assetid: 93de56b6-4ae8-4cca-acdc-25a434623509
topic_type:
- apiref
ms.openlocfilehash: 0d4c769c9f1b571296cbfe159057df083a6d5ca6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762273"
---
# <a name="isymunmanagedwriterinitialize2-method"></a>Método ISymUnmanagedWriter::Initialize2

Define a interface do emissor de metadados com a qual esse gravador será associado e define o nome do arquivo de saída para o qual os símbolos de depuração serão gravados. Esse método também permite que você defina o local final do arquivo de banco de dados do programa (PDB).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Initialize2(  
    [in] IUnknown     *emitter,  
    [in] const WCHAR  *tempfilename,  
    [in] IStream      *pIStream,  
    [in] BOOL         fFullBuild,  
    [in] const WCHAR  *finalfilename);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `emitter`  
 no Um ponteiro para a interface do emissor de metadados.  
  
 `tempfilename`  
 no Um ponteiro para um `WCHAR` que contém o nome do arquivo para o qual os símbolos de depuração são gravados. Se um nome de arquivo for especificado para um gravador que não use nomes de arquivo, esse parâmetro será ignorado.  
  
 `pIStream`  
 no Se especificado, o gravador de símbolo emitirá os símbolos para o determinado em <xref:System.Runtime.InteropServices.ComTypes.IStream> vez de para o arquivo especificado no `filename` parâmetro. O `pIStream` é opcional.  
  
 `fFullBuild`  
 [in] `true` Se esta for uma recompilação completa; `false` se esta for uma compilação incremental.  
  
 `finalfilename`  
 no Um ponteiro para um `WCHAR` que é a cadeia de caracteres do caminho para o local final do arquivo PDB.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
- [Método Initialize](isymunmanagedwriter-initialize-method.md)
