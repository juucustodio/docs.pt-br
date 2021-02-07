---
description: 'Saiba mais sobre: projeções de formulação'
title: Formule projeções
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 745742df-0eda-479b-83f8-29bd8a80db96
ms.openlocfilehash: 591bc175426f08aa4273376e4c5efe370d2be756
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672069"
---
# <a name="formulate-projections"></a>Formule projeções

Os exemplos a seguir mostram como a `select` instrução em C# e a `Select` instrução em Visual Basic podem ser combinadas com outros recursos para formar projeções de consulta.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a `Select` cláusula em Visual Basic ( `select` cláusula em C#) para retornar uma sequência de nomes de contato para `Customers` .  
  
 [!code-csharp[DLinqQueryExamples#57](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#57)]
 [!code-vb[DLinqQueryExamples#57](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#57)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a `Select` cláusula em Visual Basic ( `select` cláusula em C#) e *tipos anônimos* para retornar uma sequência de nomes de contato e números de telefone para o `Customers` .  
  
 [!code-csharp[DLinqQueryExamples#58](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#58)]
 [!code-vb[DLinqQueryExamples#58](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#58)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a `Select` cláusula em Visual Basic ( `select` cláusula em C#) e *tipos anônimos* para retornar uma sequência de nomes e números de telefone para os funcionários. Os `FirstName` `LastName` campos e são combinados em um único campo ( `Name` ), e o `HomePhone` campo é renomeado para `Phone` na sequência resultante.  
  
 [!code-csharp[DLinqQueryExamples#59](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#59)]
 [!code-vb[DLinqQueryExamples#59](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#59)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a `Select` cláusula em Visual Basic ( `select` cláusula em C#) e *tipos anônimos* para retornar uma sequência de todos os `ProductID` s e um valor calculado chamado `HalfPrice` . Esse valor é definido como `UnitPrice` dividido por 2.  
  
 [!code-csharp[DLinqQueryExamples#60](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#60)]
 [!code-vb[DLinqQueryExamples#60](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#60)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a `Select` cláusula em Visual Basic ( `select` cláusula em C#) e uma *instrução condicional* para retornar uma sequência de nome do produto e disponibilidade do produto.  
  
 [!code-csharp[DLinqQueryExamples#61](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#61)]
 [!code-vb[DLinqQueryExamples#61](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#61)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa uma `Select` cláusula Visual Basic ( `select` cláusula em C#) e um *tipo conhecido* (Name) para retornar uma sequência dos nomes dos funcionários.  
  
 [!code-csharp[DLinqQueryExamples#62](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#62)]
 [!code-vb[DLinqQueryExamples#62](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#62)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa `Select` e `Where` em Visual Basic ( `select` e `where` em C#) para retornar uma *sequência filtrada* de nomes de contato para clientes em Londres.  
  
 [!code-csharp[DLinqQueryExamples#63](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#63)]
 [!code-vb[DLinqQueryExamples#63](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#63)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa uma `Select` cláusula em Visual Basic ( `select` cláusula em C#) e *tipos anônimos* para retornar um *subconjunto em formato* dos dados sobre os clientes.  
  
 [!code-csharp[DLinqQueryExamples#64](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#64)]
 [!code-vb[DLinqQueryExamples#64](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#64)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa consultas aninhadas para retornar os resultados seguintes:  
  
- Uma sequência de todos os pedidos e seu `OrderID`correspondente S.  
  
- Um subsequence dos itens na ordem para que há desconto.  
  
- A quantidade de caixa salva se os custos de enviar não são incluídos.  
  
 [!code-csharp[DLinqQueryExamples#65](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#65)]
 [!code-vb[DLinqQueryExamples#65](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#65)]  
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
