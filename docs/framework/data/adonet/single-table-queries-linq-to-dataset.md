---
description: 'Saiba mais sobre: consultas de Single-Table (LINQ to DataSet)'
title: Consultas de tabela única (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0b74bcf8-3f87-449f-bff7-6bcb0d69d212
ms.openlocfilehash: a4b6ce2a60eeafc9221d838d1b86c9964774df60
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718753"
---
# <a name="single-table-queries-linq-to-dataset"></a>Consultas de tabela única (LINQ to DataSet)

As consultas do Language-Integrated Query (LINQ) funcionam em fontes de dados que implementam a <xref:System.Collections.Generic.IEnumerable%601> interface ou a <xref:System.Linq.IQueryable%601> interface. A <xref:System.Data.DataTable> classe não implementa nenhuma interface, portanto, você deve chamar o <xref:System.Data.DataTableExtensions.AsEnumerable%2A> método se quiser usar o <xref:System.Data.DataTable> como uma origem na `From` cláusula de uma consulta LINQ.  
  
 O exemplo a seguir obtém todos os pedidos online da tabela SalesOrderHeader e gera a identificação do pedido, a data do pedido e o número de ordem para o console.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Where1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#where1)]  
 [!code-vb[DP LINQ to DataSet Examples#Where1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#where1)]
  
 A consulta de variável local é inicializada com uma expressão de consulta, que opera em uma ou mais fontes de informações aplicando um ou mais operadores de consulta dos operadores de consulta padrão ou, no caso de LINQ to DataSet, operadores específicos para a <xref:System.Data.DataSet> classe. A expressão de consulta no exemplo anterior usa dois dos operadores de consulta padrão: `Where` e `Select`.  
  
 A cláusula `Where` filtra a sequência com base em uma condição, nesse caso de que `OnlineOrderFlag` seja definido como `true`. O operador `Select` aloca e retorna um objeto enumerável que captura os argumentos passados para o operador. Nesse exemplo acima, um tipo anônimo é criado com três propriedades: `SalesOrderID`, `OrderDate` e `SalesOrderNumber`. Os valores dessas três propriedades são definidos como os valores das colunas `SalesOrderID`, `OrderDate` e `SalesOrderNumber` da tabela `SalesOrderHeader`.  
  
 O loop `foreach` em seguida enumera o objeto enumerável retornado por `Select` e produz os resultados da consulta. Como a consulta é um tipo <xref:System.Linq.Enumerable>, que implementa <xref:System.Collections.Generic.IEnumerable%601>, a avaliação da consulta é adiada até que a variável de consulta seja iterada usando o loop `foreach`. A avaliação da consulta adiada permite que as consultas sejam mantidas como valores que podem ser avaliados várias vezes, cada vez rendendo resultados potencialmente diferentes.  
  
 O método <xref:System.Data.DataRowExtensions.Field%2A> fornece acesso aos valores de coluna de um <xref:System.Data.DataRow> e o <xref:System.Data.DataRowExtensions.SetField%2A> (não mostrado no exemplo anterior) define valores de coluna em um <xref:System.Data.DataRow>. O <xref:System.Data.DataRowExtensions.Field%2A> método e o <xref:System.Data.DataRowExtensions.SetField%2A> método tratam tipos de valor anuláveis, portanto, você não precisa verificar explicitamente se há valores nulos. Ambos os métodos também são genéricos, o que significa que você não tem que converter o tipo de retorno. Você pode usar o acessador pré-existente de coluna em <xref:System.Data.DataRow> (por exemplo, `o["OrderDate"]`), mas fazer isso exige que você converta o objeto de retorno para o tipo apropriado.  Se a coluna for um tipo de valor anulável, você precisará verificar se o valor é nulo usando o <xref:System.Data.DataRow.IsNull%2A> método. Para obter mais informações, consulte [Generic Field e métodos SetField](generic-field-and-setfield-methods-linq-to-dataset.md).  
  
 Observe que o tipo de dados especificado no parâmetro genérico `T` dos métodos <xref:System.Data.DataRowExtensions.Field%2A> e <xref:System.Data.DataRowExtensions.SetField%2A> deve corresponder ao tipo do valor subjacente ou <xref:System.InvalidCastException> será gerado. O nome da coluna especificado também deve corresponder ao nome de uma coluna no <xref:System.Data.DataSet> ou <xref:System.ArgumentException> será gerado. Em ambos os casos, a exceção é gerada na enumeração de dados em tempo de execução quando a consulta é executada.  
  
## <a name="see-also"></a>Consulte também

- [Consultas de tabela cruzada](cross-table-queries-linq-to-dataset.md)
- [Consultando DataSets tipados](querying-typed-datasets.md)
- [Campo genérico e métodos de SetField](generic-field-and-setfield-methods-linq-to-dataset.md)
