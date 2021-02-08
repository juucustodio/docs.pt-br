---
description: 'Saiba mais sobre a diretiva: #ExternalSource'
title: '#Diretiva ExternalSource'
ms.date: 07/20/2015
f1_keywords:
- '#Externalsource'
- '#ExternalSource'
- vb.ExternalSource
- Externalsource
- vb.#ExternalSource
- ExternalSource
helpviewer_keywords:
- ExternalSource directive (#ExternalSource)
- '#ExternalSource directive'
ms.assetid: 243bc6a2-34c3-4eeb-a776-9fd2bf988149
ms.openlocfilehash: 1f2e73aa152fbe2d97edcde912626696faacd5af
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797231"
---
# <a name="externalsource-directive"></a>Diretiva #ExternalSource

Indica um mapeamento entre linhas específicas de código-fonte e texto externo à origem.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
#ExternalSource( StringLiteral , IntLiteral )  
    [ LogicalLine+ ]  
#End ExternalSource  
```  
  
## <a name="parts"></a>Partes  

 `StringLiteral`  
 O caminho para a fonte externa.  
  
 `IntLiteral`  
 O número de linha da primeira linha da fonte externa.  
  
 `LogicalLine`  
 A linha em que o erro ocorre na fonte externa.  
  
 `#End ExternalSource`  
 Encerra o `#ExternalSource` bloco.  
  
## <a name="remarks"></a>Comentários  

 Essa diretiva é usada somente pelo compilador e pelo depurador.  
  
 Um arquivo de origem pode incluir diretivas de origem externas, que indicam um mapeamento entre linhas específicas de código no arquivo de origem e o texto externo à fonte, como um arquivo. aspx. Se forem encontrados erros no código-fonte designado durante a compilação, eles serão identificados como provenientes da fonte externa.  
  
 As diretivas de origem externa não têm nenhum efeito na compilação e não podem ser aninhadas. Eles são destinados ao uso interno somente pelo aplicativo.  
  
## <a name="see-also"></a>Consulte também

- [Compilação condicional](../../programming-guide/program-structure/conditional-compilation.md)
