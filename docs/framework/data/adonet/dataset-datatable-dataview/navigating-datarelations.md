---
description: 'Saiba mais sobre: navegando em DataRelations'
title: Navegando em DataRelations
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e673f4-9b44-45ae-aaea-c504d1cc5d3e
ms.openlocfilehash: 72d5bbb282b3b43434e528390769e1203519e8e2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651802"
---
# <a name="navigating-datarelations"></a>Navegando em DataRelations

Uma das principais funções de um <xref:System.Data.DataRelation> é permitir a navegação de um <xref:System.Data.DataTable> para outro em um <xref:System.Data.DataSet>. Isso permite que você recupere todos os <xref:System.Data.DataRow> objetos relacionados em uma **DataTable** quando recebe uma única **DataRow** de uma **DataTable** relacionada. Por exemplo, depois de estabelecer uma **DataRelation** entre uma tabela de clientes e uma tabela de pedidos, você pode recuperar todas as linhas de ordem de uma linha de cliente específica usando **GetChildRows**.  
  
 O exemplo de código a seguir cria uma **DataRelation** entre a tabela **Customers** e a tabela **Orders** de um **DataSet** e retorna todos os pedidos para cada cliente.  
  
 [!code-csharp[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/VB/source.vb#1)]  
  
 O exemplo a seguir se baseia no exemplo anterior, relacionando quatro tabelas juntas e navegando nessas relações. Como no exemplo anterior, **CustomerID** relaciona a tabela **Customers** à tabela **Orders** . Para cada cliente na tabela **Customers** , todas as linhas filho na tabela **Orders** são determinadas para retornar o número de pedidos que um cliente específico tem e seus valores de **OrderID** .  
  
 O exemplo expandido também retorna os valores das tabelas **OrderDetails** e **Products** . A tabela **pedidos** está relacionada à tabela **OrderDetails** usando **OrderID** para determinar, para cada pedido de cliente, quais produtos e quantidades foram ordenados. Como a tabela **OrderDetails** contém apenas a **ProductID** de um produto ordenado, o **OrderDetails** está relacionado aos **produtos** que usam **ProductID** para retornar o **NomeDoProduto**. Nessa relação, a tabela **produtos** é o pai e a tabela **detalhes do pedido** é o filho. Como resultado, ao iterar pela tabela **OrderDetails** , **GetParentRow** é chamado para recuperar o valor de **NomeDoProduto** relacionado.  
  
 Observe que, quando a **DataRelation** é criada para as tabelas **Customers** e **Orders** , nenhum valor é especificado para o sinalizador **createConstraints** (o padrão é **true**). Isso pressupõe que todas as linhas na tabela **Orders** têm um valor **CustomerID** que existe na tabela Parent **Customers** . Se um **CustomerID** existir na tabela **Orders** que não existe na tabela **Customers** , um <xref:System.Data.ForeignKeyConstraint> fará com que uma exceção seja gerada.  
  
 Quando a coluna filho pode conter valores que a coluna pai não contém, defina o sinalizador **createConstraints** como **false** ao adicionar a **DataRelation**. No exemplo, o sinalizador **createConstraints** é definido como **false** para a **DataRelation** entre a tabela **Orders** e a tabela **OrderDetails** . Isso permite que o aplicativo retorne todos os registros da tabela **OrderDetails** e apenas um subconjunto de registros da tabela **Orders** sem gerar uma exceção em tempo de execução. O exemplo expandido gera saída no formato a seguir.  
  
```output  
Customer ID: NORTS  
  Order ID: 10517  
        Order Date: 4/24/1997 12:00:00 AM  
           Product: Filo Mix  
          Quantity: 6  
           Product: Raclette Courdavault  
          Quantity: 4  
           Product: Outback Lager  
          Quantity: 6  
  Order ID: 11057  
        Order Date: 4/29/1998 12:00:00 AM  
           Product: Outback Lager  
          Quantity: 3  
```  
  
 O exemplo de código a seguir é um exemplo expandido em que os valores das tabelas **OrderDetails** e **Products** são retornados, com apenas um subconjunto dos registros na tabela **Orders** que está sendo retornada.  
  
 [!code-csharp[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/VB/source.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
