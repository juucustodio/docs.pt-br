---
description: 'Saiba mais sobre: interface ISymUnmanagedScope'
title: Interface ISymUnmanagedScope
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope
helpviewer_keywords:
- ISymUnmanagedScope interface [.NET Framework debugging]
ms.assetid: 3db7a220-cfe9-4810-8ca8-a094bb8e0f5b
topic_type:
- apiref
ms.openlocfilehash: f1175656fb49ee16fd1cd676d08f6ebb76f40c6d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763261"
---
# <a name="isymunmanagedscope-interface"></a>Interface ISymUnmanagedScope

Representa um escopo léxico dentro de um método.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetChildren](isymunmanagedscope-getchildren-method.md)|Obtém os filhos deste escopo.|  
|[Método GetEndOffset](isymunmanagedscope-getendoffset-method.md)|Obtém o deslocamento de fim deste escopo.|  
|[Método GetLocalCount](isymunmanagedscope-getlocalcount-method.md)|Obtém uma contagem das variáveis locais definidas neste escopo.|  
|[Método GetLocals](isymunmanagedscope-getlocals-method.md)|Obtém as variáveis locais definidas nesse escopo.|  
|[Método GetMethod](isymunmanagedscope-getmethod-method.md)|Obtém o método que contém esse escopo.|  
|[Método GetNamespaces](isymunmanagedscope-getnamespaces-method.md)|Obtém os namespaces que estão sendo usados nesse escopo.|  
|[Método GetParent](isymunmanagedscope-getparent-method.md)|Obtém o escopo pai deste escopo.|  
|[Método GetStartOffset](isymunmanagedscope-getstartoffset-method.md)|Obtém o deslocamento inicial para este escopo.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
- [Interface ISymUnmanagedScope2](isymunmanagedscope2-interface.md)
