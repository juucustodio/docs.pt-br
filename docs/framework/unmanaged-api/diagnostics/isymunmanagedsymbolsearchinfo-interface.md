---
description: 'Saiba mais sobre: interface ISymUnmanagedSymbolSearchInfo'
title: Interface ISymUnmanagedSymbolSearchInfo
ms.date: 03/30/2017
api_name:
- ISymUnmanagedSymbolSearchInfo
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedSymbolSearchInfo
helpviewer_keywords:
- ISymUnmanagedSymbolSearchInfo interface [.NET Framework debugging]
ms.assetid: 30817373-0a21-49c1-a0c4-8e8daeecb8db
topic_type:
- apiref
ms.openlocfilehash: 2f2ab198d2c54a9fcc5fa2e24b9196a38c583f81
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762975"
---
# <a name="isymunmanagedsymbolsearchinfo-interface"></a>Interface ISymUnmanagedSymbolSearchInfo

Fornece métodos que obtêm informações sobre o caminho de pesquisa. Obtenha essa interface chamando `QueryInterface` em um objeto que implementa a interface [ISymUnmanagedReader](isymunmanagedreader-interface.md) .  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetHRESULT](isymunmanagedsymbolsearchinfo-gethresult-method.md)|Obtém o HRESULT.|  
|[Método GetSearchPath](isymunmanagedsymbolsearchinfo-getsearchpath-method.md)|Obtém o caminho de pesquisa.|  
|[Método GetSearchPathLength](isymunmanagedsymbolsearchinfo-getsearchpathlength-method.md)|Obtém o comprimento do caminho de pesquisa.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
