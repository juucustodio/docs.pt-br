---
description: 'Saiba mais sobre: interface ISymUnmanagedWriter4'
title: Interface ISymUnmanagedWriter4
ms.date: 03/30/2017
ms.assetid: 4af5e8c0-987d-405e-b934-8b9e70fcae6e
ms.openlocfilehash: 3814d7e2728f28d224a4e9a6d99f699f220e8a4d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761675"
---
# <a name="isymunmanagedwriter4-interface"></a>Interface ISymUnmanagedWriter4

Interface ISymUnmanagedWriter4.  
  
## <a name="syntax"></a>Syntax  
  
```idl  
[object,uuid(BC7E3F53-F458-4C23-9DBD-A189E6E96594),pointer_default(unique)]interface ISymUnmanagedWriter4 : ISymUnmanagedWriter3  
```  
  
## <a name="methods"></a>Métodos  

 Essa interface contém os seguintes métodos:  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetDebugInfoWithPadding](isymunmanagedwriter4-getdebuginfowithpadding-method.md)|O funciona da mesma forma que o [método GetDebugInfo](isymunmanagedwriter-getdebuginfo-method.md) , exceto pelo fato de que a cadeia de caracteres de caminho é preenchida com zeros após o caractere nulo de terminação para tornar os dados da cadeia de caracteres um tamanho fixo `MAX_PATH` . O preenchimento só será fornecido se o comprimento da cadeia de caracteres do caminho for menor que `MAX_PATH` .<br /><br /> Isso facilita a gravação de ferramentas que diferenciam arquivos PE.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
- [Interface ISymUnmanagedWriter3](isymunmanagedwriter3-interface.md)
