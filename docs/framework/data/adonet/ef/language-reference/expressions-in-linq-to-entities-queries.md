---
description: 'Saiba mais sobre: expressões em LINQ to Entities consultas'
title: Expressões em consultas LINQ to Entities
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d70b502f-6a15-4120-b4fe-500b173ad9cc
ms.openlocfilehash: 3ab9e04adb7e823538638ae262f0e481b6948a24
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786362"
---
# <a name="expressions-in-linq-to-entities-queries"></a>Expressões em consultas LINQ to Entities

Uma expressão é um fragmento de código que pode ser avaliado como um único valor, objeto, método ou namespace. As expressões podem conter um valor literal, uma chamada de método, um operador e seus operandos ou um nome simples. Os nomes simples podem ser o nome de uma variável, um membro de tipo, um parâmetro de método, um namespace ou um tipo. As expressões podem usar operadores que, por sua vez, usam outras expressões como parâmetros ou chamadas de métodos cujos parâmetros são, por sua vez, outras chamadas de métodos. Portanto, as expressões podem variar de simples a muito complexas.  
  
 Em consultas LINQ to Entities, as expressões podem conter qualquer coisa permitida pelos tipos dentro do <xref:System.Linq.Expressions> namespace, incluindo expressões lambda. As expressões que podem ser usadas em LINQ to Entities consultas são um superconjunto das expressões que podem ser usadas para consultar o Entity Framework. as expressões que fazem parte das consultas no Entity Framework são limitadas às operações com suporte `ObjectQuery<T>` no e na fonte de dados subjacente.  
  
 No exemplo a seguir, a comparação na cláusula `Where` é uma expressão:  
  
 [!code-csharp[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#whereexpression)]
 [!code-vb[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#whereexpression)]  
  
> [!NOTE]
> Construções de linguagem específicas, como C# `unchecked` , não têm significado em LINQ to Entities.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Expressões constantes](constant-expressions.md)  
  
 [Expressões de Comparação](comparison-expressions.md)  
  
 [Comparações nulas](null-comparisons.md)  
  
 [Expressões de inicialização](initialization-expressions.md)  
  
 [Relações, propriedades de navegação e chaves estrangeiras](/ef/ef6/fundamentals/relationships)  
  
## <a name="see-also"></a>Consulte também

- [ADO.NET Entity Framework](../index.md)
