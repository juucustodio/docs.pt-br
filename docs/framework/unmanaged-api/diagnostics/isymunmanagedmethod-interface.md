---
description: 'Saiba mais sobre: interface ISymUnmanagedMethod'
title: Interface ISymUnmanagedMethod
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod
helpviewer_keywords:
- ISymUnmanagedMethod interface [.NET Framework debugging]
ms.assetid: f204d74c-cc79-4092-83bb-60654be95649
topic_type:
- apiref
ms.openlocfilehash: 18f87784a959ddc62415592e51d1971ea10f90bf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709952"
---
# <a name="isymunmanagedmethod-interface"></a>Interface ISymUnmanagedMethod

Representa um método dentro do repositório de símbolos. Essa interface fornece acesso apenas aos atributos relacionados a símbolos de um método, em vez dos atributos relacionados ao tipo.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetNamespace](isymunmanagedmethod-getnamespace-method.md)|Obtém o namespace no qual esse método é definido.|  
|[Método GetOffset](isymunmanagedmethod-getoffset-method.md)|Retorna o deslocamento dentro desse método que corresponde a uma determinada posição dentro de um documento.|  
|[Método GetParameters](isymunmanagedmethod-getparameters-method.md)|Obtém os parâmetros para este método.|  
|[Método GetRanges](isymunmanagedmethod-getranges-method.md)|Dada uma posição em um documento, retorna uma matriz de pares de deslocamento inicial e final que correspondem aos intervalos da MSIL (Microsoft Intermediate Language) que a posição aborda nesse método.|  
|[Método GetRootScope](isymunmanagedmethod-getrootscope-method.md)|Obtém o escopo léxico raiz dentro deste método. Esse escopo abrange todo o método.|  
|[Método GetScopeFromOffset](isymunmanagedmethod-getscopefromoffset-method.md)|Obtém o escopo léxico mais delimitador dentro desse método que envolve o deslocamento fornecido.|  
|[Método GetSequencePointCount](isymunmanagedmethod-getsequencepointcount-method.md)|Obtém a contagem de pontos de sequência dentro deste método.|  
|[Método GetSequencePoints](isymunmanagedmethod-getsequencepoints-method.md)|Obtém todos os pontos de sequência dentro deste método.|  
|[Método GetSourceStartEnd](isymunmanagedmethod-getsourcestartend-method.md)|Obtém as posições do documento inicial e final da origem deste método.|  
|[Método GetToken](isymunmanagedmethod-gettoken-method.md)|Retorna o token de metadados para esse método.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
