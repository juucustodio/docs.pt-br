---
description: 'Saiba mais sobre: cláusula Let (Visual Basic)'
title: Cláusula Let
ms.date: 07/20/2015
f1_keywords:
- vb.QueryLet
helpviewer_keywords:
- queries [Visual Basic], Let
- Let clause [Visual Basic]
- Let statement [Visual Basic]
ms.assetid: 981aa516-16eb-4c53-b1f1-5aa3e82f316e
ms.openlocfilehash: 88a7d96bb790a1e6ec5adfa4337c51f807930168
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99653635"
---
# <a name="let-clause-visual-basic"></a>Cláusula Let (Visual Basic)

Computa um valor e o atribui a uma nova variável dentro da consulta.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Let variable = expression [, ...]  
```  
  
## <a name="parts"></a>Partes  
  
|Termo|Definição|  
|---|---|  
|`variable`|Obrigatório. Um alias que pode ser usado para referenciar os resultados da expressão fornecida.|  
|`expression`|Obrigatório. Uma expressão que será avaliada e atribuída à variável especificada.|  
  
## <a name="remarks"></a>Comentários  

 A `Let` cláusula permite que você calcule valores para cada resultado de consulta e faça referência a eles usando um alias. O alias pode ser usado em outras cláusulas, como a `Where` cláusula. A `Let` cláusula permite que você crie uma instrução de consulta que seja mais fácil de ler, pois você pode especificar um alias para uma cláusula de expressão incluído na consulta e substituir o alias sempre que a cláusula de expressão for usada.  
  
 Você pode incluir qualquer número de `variable` `expression` atribuições e na `Let` cláusula. Separe cada atribuição com uma vírgula (,).  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir usa a `Let` cláusula para calcular um desconto de 10% nos produtos.  
  
 [!code-vb[VbSimpleQuerySamples#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#16)]  
  
## <a name="see-also"></a>Consulte também

- [Introdução a LINQ no Visual Basic](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [Consultas](index.md)
- [Cláusula SELECT](select-clause.md)
- [Cláusula from](from-clause.md)
- [Cláusula WHERE](where-clause.md)
