---
description: 'Saiba mais sobre: cláusula Skip (Visual Basic)'
title: Cláusula Skip
ms.date: 07/20/2015
f1_keywords:
- vb.QuerySkip
helpviewer_keywords:
- queries [Visual Basic], Skip
- Skip statement [Visual Basic]
- Skip clause [Visual Basic]
ms.assetid: f00eb172-3907-4c43-9745-d8546ab86234
ms.openlocfilehash: 6af702f65a724ea8c3d5a6122fb5f7a0ed5f6755
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99653544"
---
# <a name="skip-clause-visual-basic"></a>Cláusula Skip (Visual Basic)

Ignora um número especificado de elementos em uma coleção e, em seguida, retorna os elementos restantes.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Skip count  
```  
  
## <a name="parts"></a>Partes  

 `count`  
 Obrigatório. Um valor ou uma expressão que é avaliada como o número de elementos da sequência a serem ignorados.  
  
## <a name="remarks"></a>Comentários  

 A `Skip` cláusula faz com que uma consulta ignore os elementos no início de uma lista de resultados e retorne os elementos restantes. O número de elementos a serem ignorados é identificado pelo `count` parâmetro.  
  
 Você pode usar a `Skip` cláusula com a `Take` cláusula para retornar um intervalo de dados de qualquer segmento de uma consulta. Para fazer isso, passe o índice do primeiro elemento do intervalo para a `Skip` cláusula e o tamanho do intervalo para a `Take` cláusula.  
  
 Quando você usa a `Skip` cláusula em uma consulta, também pode ser necessário garantir que os resultados sejam retornados em uma ordem que permitirá que a `Skip` cláusula ignore os resultados pretendidos. Para obter mais informações sobre como ordenar os resultados da consulta, consulte [cláusula order by](order-by-clause.md).  
  
 Você pode usar a `SkipWhile` cláusula para especificar que apenas determinados elementos sejam ignorados, dependendo de uma condição fornecida.  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir usa a `Skip` cláusula junto com a `Take` cláusula para retornar dados de uma consulta em páginas. A `GetCustomers` função usa a `Skip` cláusula para ignorar os clientes na lista até o valor de índice inicial fornecido e usa a `Take` cláusula para retornar uma página de clientes que inicia com esse valor de índice.  
  
 [!code-vb[VbSimpleQuerySamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Introdução a LINQ no Visual Basic](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [Consultas](index.md)
- [Cláusula SELECT](select-clause.md)
- [Cláusula from](from-clause.md)
- [Cláusula order by](order-by-clause.md)
- [Cláusula Skip While](skip-while-clause.md)
- [Cláusula Take](take-clause.md)
