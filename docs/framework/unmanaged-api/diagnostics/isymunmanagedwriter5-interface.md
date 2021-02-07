---
description: 'Saiba mais sobre: interface ISymUnmanagedWriter5'
title: Interface ISymUnmanagedWriter5
ms.date: 03/30/2017
ms.assetid: 15b8526e-4f5d-475c-a1e3-d8b2d145c879
ms.openlocfilehash: 0902385576e1eed17cea672b04858c7e3ef7add8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761623"
---
# <a name="isymunmanagedwriter5-interface"></a>Interface ISymUnmanagedWriter5

Interface ISymUnmanagedWriter5.  
  
## <a name="syntax"></a>Syntax  
  
```idl  
[object,uuid(DCF7780D-BDE9-45DF-ACFE-21731A32000C),pointer_default(unique)]interface ISymUnmanagedWriter5 : ISymUnmanagedWriter4  
```  
  
## <a name="methods"></a>Métodos  

 Essa interface contém os seguintes métodos:  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CloseMapTokensToSourceSpans](isymunmanagedwriter5-closemaptokenstosourcespans-method.md)|Feche a seção de dados personalizados especiais para obter informações de mapeamento de token para origem. Depois de fechada, não é possível adicionar mais informações de mapeamento.|  
|[Método MapTokenToSourceSpan](isymunmanagedwriter5-maptokentosourcespan-method.md)|Mapeia o token de metadados fornecido para o span de linha de origem fornecido no arquivo de origem especificado.<br /><br /> Deve ser chamado entre as chamadas para o [método OpenMapTokensToSourceSpans](isymunmanagedwriter5-openmaptokenstosourcespans-method.md) e o [método CloseMapTokensToSourceSpans](isymunmanagedwriter5-closemaptokenstosourcespans-method.md).|  
|[Método OpenMapTokensToSourceSpans](isymunmanagedwriter5-openmaptokenstosourcespans-method.md)|Abra uma seção especial de dados personalizados para emitir informações de mapeamento de extensão de token para origem no. Abrir esta seção quando um método já estiver aberto, ou vice-versa, é um erro.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
- [Interface ISymUnmanagedWriter4](isymunmanagedwriter4-interface.md)
