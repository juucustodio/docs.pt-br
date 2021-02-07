---
description: 'Saiba mais sobre: método ISymUnmanagedWriter:: Initialize'
title: Método ISymUnmanagedWriter::Initialize
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.Initialize
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::Initialize
helpviewer_keywords:
- ISymUnmanagedWriter::Initialize method [.NET Framework debugging]
- Initialize method, ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: e0ebd793-3764-4df0-8f12-0e95f60b9eae
topic_type:
- apiref
ms.openlocfilehash: eab60e9539df3d43a1602268d704ac324f028915
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762286"
---
# <a name="isymunmanagedwriterinitialize-method"></a>Método ISymUnmanagedWriter::Initialize

Define a interface do emissor de metadados com a qual esse gravador será associado e define o nome do arquivo de saída para o qual os símbolos de depuração serão gravados.  
  
 Esse método pode ser chamado apenas uma vez e deve ser chamado antes de qualquer outro método de gravador. Alguns gravadores podem exigir um nome de arquivo. No entanto, você sempre pode passar um nome de arquivo para esse método sem nenhum efeito negativo nos gravadores que não usam o nome do arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Initialize(  
    [in] IUnknown     *emitter,  
    [in] const WCHAR  *filename,  
    [in] IStream      *pIStream,  
    [in] BOOL         fFullBuild);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `emitter`  
 no Um ponteiro para a interface do emissor de metadados.  
  
 `filename`  
 no O nome do arquivo para o qual os símbolos de depuração são gravados. Se um nome de arquivo for especificado para um gravador que não use nomes de arquivo, esse parâmetro será ignorado.  
  
 `pIStream`  
 no Se especificado, o gravador de símbolo emitirá os símbolos para o determinado em <xref:System.Runtime.InteropServices.ComTypes.IStream> vez de para o arquivo especificado no `filename` parâmetro. O `pIStream` é opcional.  
  
 `fFullBuild`  
 [in] `true` Se esta for uma recompilação completa; `false` se esta for uma compilação incremental.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
- [Método Initialize2](isymunmanagedwriter-initialize2-method.md)
