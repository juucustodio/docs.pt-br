---
description: 'Saiba mais sobre: ISymUnmanagedWriter: método efineParameter de:D'
title: Método ISymUnmanagedWriter::DefineParameter
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineParameter
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineParameter
helpviewer_keywords:
- DefineParameter method [.NET Framework debugging]
- ISymUnmanagedWriter::DefineParameter method [.NET Framework debugging]
ms.assetid: a8e3dd32-6a44-4371-9a74-f417b11998c8
topic_type:
- apiref
ms.openlocfilehash: 1e42140e33a99b224ccf3eff7ea29b7aa3ff1b15
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762351"
---
# <a name="isymunmanagedwriterdefineparameter-method"></a>Método ISymUnmanagedWriter::DefineParameter

Define um único parâmetro no método atual. O tipo de parâmetro é obtido da posição do parâmetro (sequência) na assinatura do método.  
  
 Se os parâmetros forem definidos nos metadados de um determinado método, você não precisará defini-los novamente usando esse método. Os leitores de símbolo devem verificar os metadados normais dos parâmetros antes de verificar o repositório de símbolos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineParameter(  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] ULONG32      sequence,  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `name`  
 no O nome do parâmetro.  
  
 `attributes`  
 no Os atributos de parâmetro.  
  
 `sequence`  
 no A assinatura do parâmetro.  
  
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
