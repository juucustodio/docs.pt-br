---
description: 'Saiba mais sobre: ignorar cláusula while (Visual Basic)'
title: Cláusula Skip While
ms.date: 07/20/2015
f1_keywords:
- vb.QuerySkipWhile
helpviewer_keywords:
- Skip While statement [Visual Basic]
- Skip While clause [Visual Basic]
- queries [Visual Basic], Skip While
ms.assetid: 5dee8350-7520-4f1a-b00d-590cacd572d6
ms.openlocfilehash: 6f2785fde1a62c10c914904ccba51510dbb1a041
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99773843"
---
# <a name="skip-while-clause-visual-basic"></a>Ignorar cláusula While (Visual Basic)

Ignora os elementos em uma coleção, desde que uma condição especificada seja `true` e, em seguida, retorne os elementos restantes.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Skip While expression  
```  
  
## <a name="parts"></a>Partes  
  
|Termo|Definição|  
|---|---|  
|`expression`|Obrigatório. Uma expressão que representa uma condição para os elementos de teste. A expressão deve retornar um `Boolean` valor ou um equivalente funcional, como um `Integer` a ser avaliado como um `Boolean` .|  
  
## <a name="remarks"></a>Comentários  

 A `Skip While` cláusula ignora os elementos do início de um resultado da consulta até que o `expression` retorno fornecido `false` . Após o `expression` retorno `false` , a consulta retorna todos os elementos restantes. O `expression` é ignorado para os resultados restantes.  
  
 A `Skip While` cláusula é diferente da cláusula, pois `Where` a `Where` cláusula pode ser usada para excluir todos os elementos de uma consulta que não atendem a uma condição específica. A `Skip While` cláusula exclui elementos somente até a primeira vez que a condição não for satisfeita. A `Skip While` cláusula é mais útil quando você está trabalhando com um resultado de consulta ordenado.  
  
 Você pode ignorar um número específico de resultados do início de um resultado de consulta usando a `Skip` cláusula.  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir usa a `Skip While` cláusula para ignorar os resultados até que o primeiro cliente do Estados Unidos seja encontrado.  
  
 [!code-vb[VbSimpleQuerySamples#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- [Introdução a LINQ no Visual Basic](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [Consultas](index.md)
- [Cláusula SELECT](select-clause.md)
- [Cláusula from](from-clause.md)
- [Cláusula Skip](skip-clause.md)
- [Cláusula Take While](take-while-clause.md)
- [Cláusula WHERE](where-clause.md)
