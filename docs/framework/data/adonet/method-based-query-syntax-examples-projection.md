---
description: 'Saiba mais sobre: Method-Based exemplos de sintaxe de consulta: projeção (LINQ to DataSet)'
title: 'Exemplos de sintaxe da consulta com base em método: Projeção (LINQ to DataSet)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0fc2c8f0-1967-4f30-8b20-39b8dccfb82f
ms.openlocfilehash: 380c35962ed122f5d4bbe85ba3fbd87cf7d7a3bf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754375"
---
# <a name="method-based-query-syntax-examples-projection-linq-to-dataset"></a>Exemplos de sintaxe da consulta com base em método: Projeção (LINQ to DataSet)

Os exemplos neste tópico demonstram como usar os métodos de <xref:System.Linq.Enumerable.Select%2A> e de <xref:System.Linq.Enumerable.SelectMany%2A> para ver <xref:System.Data.DataSet> usando a sintaxe da consulta com base em método.  
  
 O `FillDataSet` método usado nesses exemplos é especificado no [carregamento de dados em um conjunto](loading-data-into-a-dataset.md).  
  
 Os exemplos neste tópico usam as tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 Para obter mais informações, consulte [como: criar um projeto de LINQ to DataSet no Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).  
  
## <a name="select"></a>Selecionar  
  
### <a name="example"></a>Exemplo  

 Este exemplo usa o método de <xref:System.Linq.Enumerable.Select%2A> para projetar `Name`, `ProductNumber`, e propriedades de `ListPrice` como uma sequência de tipos anônimos.  A propriedade de `ListPrice` é renomeada também a `Price` no tipo resultante.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectAnonymousTypes_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectanonymoustypes_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SelectAnonymousTypes_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectanonymoustypes_mq)]  
  
## <a name="selectmany"></a>SelectMany  
  
### <a name="example"></a>Exemplo  

 Este exemplo usa o método de <xref:System.Linq.Enumerable.SelectMany%2A> para selecionar todos os pedidos onde `TotalDue` é menor que 500,00.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectManyCompoundFrom_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectmanycompoundfrom_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SelectManyCompoundFrom_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectmanycompoundfrom_mq)]  
  
### <a name="example"></a>Exemplo  

 Este exemplo usa o método de <xref:System.Linq.Enumerable.SelectMany%2A> para selecionar todos os pedidos na ordem foi feito o 1º de outubro de 2002 ou posterior.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectManyCompoundFrom2_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectmanycompoundfrom2_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SelectManyCompoundFrom2_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectmanycompoundfrom2_mq)]  
  
## <a name="see-also"></a>Consulte também

- [Carregando dados em um DataSet](loading-data-into-a-dataset.md)
- [LINQ para exemplos de DataSet](linq-to-dataset-examples.md)
- [Visão geral de operadores de consulta padrão (C#)](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Visão geral de operadores de consulta padrão (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
