---
description: 'Saiba mais sobre o método: ISymUnmanagedWriter:: SetSymAttribute'
title: Método ISymUnmanagedWriter::SetSymAttribute
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.SetSymAttribute
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::SetSymAttribute
helpviewer_keywords:
- SetSymAttribute method [.NET Framework debugging]
- ISymUnmanagedWriter::SetSymAttribute method [.NET Framework debugging]
ms.assetid: 64d9b80e-b883-4539-89c7-03573185a1eb
topic_type:
- apiref
ms.openlocfilehash: 0509e6430646fa67112b29d30d5053eb4a541415
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761987"
---
# <a name="isymunmanagedwritersetsymattribute-method"></a>Método ISymUnmanagedWriter::SetSymAttribute

Define um atributo personalizado com base no seu nome. Esses atributos são mantidos no repositório de símbolos, ao contrário dos atributos personalizados de metadados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetSymAttribute(  
    [in] mdToken parent,  
    [in] const WCHAR *name,  
    [in] ULONG32 cData,  
    [in, size_is(cData)] unsigned char data[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `parent`  
 no O token de metadados para o qual o atributo está sendo definido.  
  
 `name`  
 no Um ponteiro para um `WCHAR` que contém o nome do atributo.  
  
 `cData`  
 no Um `ULONG32` que indica o tamanho da `data` matriz.  
  
 `data`  
 no O valor do atributo.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
