---
description: 'Saiba mais sobre: exemplos de operador de DataSet-Specific (LINQ to DataSet)'
title: Exemplos Conjunto de dados específicos de operador (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8fdd64af-6ad0-46cd-91c8-dbe26620eeb1
ms.openlocfilehash: 2fd54453621ce180901aaf6fbb5b975067ad9831
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651321"
---
# <a name="dataset-specific-operator-examples-linq-to-dataset"></a>Exemplos Conjunto de dados específicos de operador (LINQ to DataSet)

Os exemplos neste tópico demonstram como usar o método de <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> e a classe de <xref:System.Data.DataRowComparer> .  
  
 O `FillDataSet` método usado nesses exemplos é especificado no [carregamento de dados em um conjunto](loading-data-into-a-dataset.md).  
  
 Os exemplos neste tópico usam as tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 Para obter mais informações, consulte [como: criar um projeto de LINQ to DataSet no Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).  
  
## <a name="copytodatatable"></a>CopyToDataTable  
  
### <a name="example"></a>Exemplo  

 Este exemplo carrega <xref:System.Data.DataTable> com resultados de consulta usando o método <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> .  
  
 [!code-csharp[DP LINQ to DataSet Examples#LoadDataTableWithQueryResults](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#loaddatatablewithqueryresults)]
 [!code-vb[DP LINQ to DataSet Examples#LoadDataTableWithQueryResults](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#loaddatatablewithqueryresults)]  
  
## <a name="datarowcomparer"></a>DataRowComparer  
  
### <a name="example"></a>Exemplo  

 Este exemplo compara duas linhas de dados diferentes usando <xref:System.Data.DataRowComparer>.  
  
 [!code-csharp[DP LINQ to DataSet Examples#CompareDifferentDataRows](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#comparedifferentdatarows)]  
  
## <a name="see-also"></a>Consulte também

- [Carregando dados em um DataSet](loading-data-into-a-dataset.md)
- [LINQ para exemplos de DataSet](linq-to-dataset-examples.md)
