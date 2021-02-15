---
description: 'Saiba mais sobre: interface ISymENCUnmanagedMethod'
title: Interface ISymENCUnmanagedMethod
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod
helpviewer_keywords:
- ISymENCUnmanagedMethod interface [.NET Framework debugging]
ms.assetid: faebf594-67d5-4abf-b9c1-547fd3a1ff87
topic_type:
- apiref
ms.openlocfilehash: 59dd56c20279b2507fc4432182d0abb5b3e9c289
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790315"
---
# <a name="isymencunmanagedmethod-interface"></a>Interface ISymENCUnmanagedMethod

Fornece informações para o recurso Editar e continuar.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetDocumentsForMethod](isymencunmanagedmethod-getdocumentsformethod-method.md)|Obtém os documentos em que este método tem linhas.|  
|[Método GetDocumentsForMethodCount](isymencunmanagedmethod-getdocumentsformethodcount-method.md)|Obtém o número de documentos em que esse método tem linhas.|  
|[Método GetFileNameFromOffset](isymencunmanagedmethod-getfilenamefromoffset-method.md)|Obtém o nome do arquivo da linha associada a um deslocamento.|  
|[Método GetLineFromOffset](isymencunmanagedmethod-getlinefromoffset-method.md)|Obtém as informações de linha associadas a um deslocamento.|  
|[Método GetSourceExtentInDocument](isymencunmanagedmethod-getsourceextentindocument-method.md)|Obtém a menor linha inicial e a linha final maior para o método em um documento específico.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
