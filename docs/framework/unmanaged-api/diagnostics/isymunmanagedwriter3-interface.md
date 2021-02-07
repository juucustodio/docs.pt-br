---
description: 'Saiba mais sobre: interface ISymUnmanagedWriter3'
title: Interface ISymUnmanagedWriter3
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter3
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter3
helpviewer_keywords:
- ISymUnmanagedWriter3 interface [.NET Framework debugging]
ms.assetid: a034c21e-e371-4360-b470-29e88288948f
topic_type:
- apiref
ms.openlocfilehash: 586220af85f193b43acf0578706d9f67e3e83386
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761727"
---
# <a name="isymunmanagedwriter3-interface"></a>Interface ISymUnmanagedWriter3

Representa um gravador de símbolo e fornece métodos para definir documentos, pontos de sequência, escopos lexicais e variáveis. Essa interface estende a interface [ISymUnmanagedWriter](isymunmanagedwriter-interface.md) .  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Commit](isymunmanagedwriter3-commit-method.md)|Confirma as alterações gravadas até o fluxo.|  
|[Método OpenMethod2](isymunmanagedwriter3-openmethod2-method.md)|Abre um método e fornece seu deslocamento de seção real na imagem.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
- [Interface ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
- [Interface ISymUnmanagedWriter2](isymunmanagedwriter2-interface.md)
