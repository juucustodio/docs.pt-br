---
description: 'Saiba mais sobre: ISymUnmanagedWriter: método efineLocalVariable de:D'
title: Método ISymUnmanagedWriter::DefineLocalVariable
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineLocalVariable
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineLocalVariable
helpviewer_keywords:
- ISymUnmanagedWriter::DefineLocalVariable method [.NET Framework debugging]
- DefineLocalVariable method [.NET Framework debugging]
ms.assetid: 6fab8a58-3883-490f-8b27-64042c90f104
topic_type:
- apiref
ms.openlocfilehash: cd817e3002c2a55fd8bbd7e565283752926f746b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762364"
---
# <a name="isymunmanagedwriterdefinelocalvariable-method"></a>Método ISymUnmanagedWriter::DefineLocalVariable

Define uma única variável no escopo léxico atual. Esse método pode ser chamado várias vezes para uma variável do mesmo nome que tem várias casas em um escopo. Nesse caso, no entanto, os valores dos `startOffset` `endOffset` parâmetros e não devem se sobrepor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineLocalVariable(  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] ULONG32      cSig,  
    [in, size_is(cSig)] unsigned char signature[],  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3,  
    [in] ULONG32      startOffset,  
    [in] ULONG32      endOffset);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `name`  
 no Um ponteiro para um `WCHAR` que define o nome da variável local.  
  
 `attributes`  
 no Os atributos da variável local.  
  
 `cSig`  
 no Um `ULONG32` que indica o tamanho, em bytes, do `signature` buffer.  
  
 `signature`  
 no A assinatura da variável local.  
  
 `addrKind`  
 no O tipo de endereço.  
  
 `addr1`  
 no O primeiro endereço para a especificação de parâmetro.  
  
 `addr2`  
 no O segundo endereço para a especificação de parâmetro.  
  
 `addr3`  
 no O terceiro endereço para a especificação de parâmetro.  
  
 `startOffset`  
 no O deslocamento de início da variável. Esse parâmetro é opcional. Se for 0, esse parâmetro será ignorado e a variável será definida em todo o escopo. Se for um valor diferente de zero, a variável se enquadrará dentro dos deslocamentos do escopo atual.  
  
 `endOffset`  
 no O deslocamento de fim da variável. Esse parâmetro é opcional. Se for 0, esse parâmetro será ignorado e a variável será definida em todo o escopo. Se for um valor diferente de zero, a variável se enquadrará dentro dos deslocamentos do escopo atual.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
- [Método DefineGlobalVariable](isymunmanagedwriter-defineglobalvariable-method.md)
- [Método DefineLocalVariable2](isymunmanagedwriter2-definelocalvariable2-method.md)
