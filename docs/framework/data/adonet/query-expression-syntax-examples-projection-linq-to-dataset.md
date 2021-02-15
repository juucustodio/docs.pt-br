---
description: 'Saiba mais sobre: exemplos de sintaxe de expressão de consulta: projeção (LINQ to DataSet)'
title: 'Exemplos de sintaxe de expressão de consulta: projeção (LINQ to DataSet)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 48c9f5ed-76bf-4228-ab10-5217bbb295a3
ms.openlocfilehash: 710426108304d5b3fa38004fb37d234ed206733c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663515"
---
# <a name="query-expression-syntax-examples-projection--linq-to-dataset"></a>Exemplos de sintaxe de expressão de consulta: projeção (LINQ to DataSet)

Os exemplos neste tópico demonstram como usar os métodos <xref:System.Linq.Enumerable.Select%2A> e <xref:System.Linq.Enumerable.SelectMany%2A> para consultar um <xref:System.Data.DataSet> usando a sintaxe de expressão de consulta.  
  
 O `FillDataSet` método usado nesses exemplos é especificado no [carregamento de dados em um conjunto](loading-data-into-a-dataset.md).  
  
 Os exemplos neste tópico usam as tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 Para obter mais informações, consulte [como: criar um projeto de LINQ to DataSet no Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).  
  
## <a name="select"></a>Selecionar  
  
### <a name="example"></a>Exemplo  

 Este exemplo usa o método <xref:System.Linq.Enumerable.Select%2A> para retornar todas as linhas da tabela de `Product` e exibir os nomes de produto.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectSimple1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectsimple1)]
 [!code-vb[DP LINQ to DataSet Examples#SelectSimple1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectsimple1)]  
  
### <a name="example"></a>Exemplo  

 Este exemplo usa <xref:System.Linq.Enumerable.Select%2A> para retornar somente uma sequência de nomes do produto.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectSimple2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectsimple2)]
 [!code-vb[DP LINQ to DataSet Examples#SelectSimple2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectsimple2)]  
  
## <a name="selectmany"></a>SelectMany  
  
### <a name="example"></a>Exemplo  

 Este exemplo usa `From …, …` (o equivalente do método <xref:System.Linq.Enumerable.SelectMany%2A>) para selecionar todos os pedidos onde `TotalDue` é menor que 500,00.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectManyCompoundFrom](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectmanycompoundfrom)]
 [!code-vb[DP LINQ to DataSet Examples#SelectManyCompoundFrom](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectmanycompoundfrom)]  
  
### <a name="example"></a>Exemplo  

 Este exemplo usa `From …, …` (o equivalente do método <xref:System.Linq.Enumerable.SelectMany%2A>) para selecionar todos os pedidos feitos em 1º de outubro de 2002 ou posterior.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectManyCompoundFrom2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectmanycompoundfrom2)]
 [!code-vb[DP LINQ to DataSet Examples#SelectManyCompoundFrom2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectmanycompoundfrom2)]  
  
### <a name="example"></a>Exemplo  

 Este exemplo usa `From …, …` (o equivalente do método <xref:System.Linq.Enumerable.SelectMany%2A>) para selecionar todos os pedidos onde o total do pedido é maior que 10000,00 e usa a atribuição `From` para evitar solicitar o total duas vezes.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectManyFromAssignment](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectmanyfromassignment)]
 [!code-vb[DP LINQ to DataSet Examples#SelectManyFromAssignment](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectmanyfromassignment)]  
  
## <a name="see-also"></a>Consulte também

- [Carregando dados em um DataSet](loading-data-into-a-dataset.md)
- [LINQ para exemplos de DataSet](linq-to-dataset-examples.md)
- [Visão geral de operadores de consulta padrão (C#)](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Visão geral de operadores de consulta padrão (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
