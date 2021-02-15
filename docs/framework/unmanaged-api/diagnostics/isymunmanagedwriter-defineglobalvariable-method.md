---
description: 'Saiba mais sobre: ISymUnmanagedWriter: método efineGlobalVariable de:D'
title: Método ISymUnmanagedWriter::DefineGlobalVariable
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineGlobalVariable
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineGlobalVariable
helpviewer_keywords:
- ISymUnmanagedWriter::DefineGlobalVariable method [.NET Framework debugging]
- DefineGlobalVariable method [.NET Framework debugging]
ms.assetid: 843c904a-8176-4d8f-bd47-b4d4c29f4c5c
topic_type:
- apiref
ms.openlocfilehash: 70dccfed054a9ac79baf3f28683edc9a14d3cdf7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762377"
---
# <a name="isymunmanagedwriterdefineglobalvariable-method"></a>Método ISymUnmanagedWriter::DefineGlobalVariable

Define uma única variável global.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineGlobalVariable(  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] ULONG32      cSig,  
    [in, size_is(cSig)] unsigned char signature[],  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `name`  
 no Um ponteiro para um `WCHAR` que define o nome da variável global.  
  
 `attributes`  
 no Os atributos da variável global.  
  
 `cSig`  
 no Um `ULONG32` que indica o tamanho, em caracteres, do `signature` buffer.  
  
 `signature`  
 no A assinatura de variável global.  
  
 `addrKind`  
 no O tipo de endereço.  
  
 `addr1`  
 no O primeiro endereço para a especificação de parâmetro.  
  
 `addr2`  
 no O segundo endereço para a especificação de parâmetro.  
  
 `addr3`  
 no O terceiro endereço para a especificação de parâmetro.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
- [Método DefineLocalVariable](isymunmanagedwriter-definelocalvariable-method.md)
- [Método DefineGlobalVariable2](isymunmanagedwriter2-defineglobalvariable2-method.md)
