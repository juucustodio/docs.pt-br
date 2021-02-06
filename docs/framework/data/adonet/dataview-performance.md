---
description: 'Saiba mais sobre: desempenho de DataView'
title: Desempenho de um DataView
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 90820e49-9d46-41f6-9a3d-6c0741bbd8eb
ms.openlocfilehash: 6319eb3846f116b0297df701e9a6abc6c1deb2b3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651282"
---
# <a name="dataview-performance"></a>Desempenho de um DataView

Este tópico aborda os benefícios de desempenho de usar <xref:System.Data.DataView.Find%2A> e métodos de <xref:System.Data.DataView.FindRows%2A> de <xref:System.Data.DataView> classe, e para armazenar em cachê <xref:System.Data.DataView> em um aplicativo da Web.  
  
## <a name="find-and-findrows"></a>Localize e FindRows  

 <xref:System.Data.DataView> constrói um índice. Um índice contém chaves criadas de uma ou mais colunas da tabela ou exibição. Essas chaves são armazenadas em uma estrutura que permite <xref:System.Data.DataView> para encontrar a linha ou linhas associada com os valores da chave rapidamente e com eficiência. As operações que usam o índice, como filtragem e classificação, confiram aumentos de desempenho significativos. O índice de um <xref:System.Data.DataView> é compilado quando <xref:System.Data.DataView> é criado e quando qualquer informação de classificação ou de filtragem é modificada. Criar <xref:System.Data.DataView> e então defina a classificação ou informações de filtragem causam posteriormente o índice a ser compilado pelo menos duas vezes: uma vez que quando <xref:System.Data.DataView> é criado, e novamente quando algumas de tipo ou propriedades de filtragem são alteradas. Para obter mais informações sobre filtragem e classificação com o <xref:System.Data.DataView> , consulte [filtrando com DataView](filtering-with-dataview-linq-to-dataset.md) e [classificando com DataView](sorting-with-dataview-linq-to-dataset.md).  
  
 Se você quiser retornar os resultados de uma consulta específica nos dados, ao contrário de fornecer uma exibição dinâmica de um subconjunto dos dados, você poderá usar os métodos <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> de <xref:System.Data.DataView>, em vez de definir a propriedade <xref:System.Data.DataView.RowFilter%2A>. A propriedade <xref:System.Data.DataView.RowFilter%2A> é melhor usada em um aplicativo associado a dados onde um controle de associação exibe resultados filtrados. Definir a propriedade <xref:System.Data.DataView.RowFilter%2A> reconstrói o índice para os dados, adicionando a sobrecarga ao seu aplicativo e diminuindo o desempenho. Os métodos <xref:System.Data.DataView.Find%2A> e <xref:System.Data.DataView.FindRows%2A> usam o índice atual sem exigir que o índice seja reconstruído. Se você chamar <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> apenas uma vez, deverá usar o <xref:System.Data.DataView> existente. Se você chamar <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> várias vezes, deverá criar um novo <xref:System.Data.DataView> para recriar o índice na coluna em que você deseja pesquisar e, em seguida, chamar os métodos <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A>. Para obter mais informações sobre <xref:System.Data.DataView.Find%2A> os <xref:System.Data.DataView.FindRows%2A> métodos e, consulte [Localizando linhas](./dataset-datatable-dataview/finding-rows.md).  
  
 O exemplo a seguir usa o método de <xref:System.Data.DataView.Find%2A> para localizar um contato com o sobrenome “Zhu”.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryOrderByFind](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromqueryorderbyfind)]
 [!code-vb[DP DataView Samples#LDVFromQueryOrderByFind](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromqueryorderbyfind)]  
  
 O exemplo a seguir usa o método de <xref:System.Data.DataView.FindRows%2A> para localizar todos os produtos colorido vermelho.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryFindRows](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromqueryfindrows)]
 [!code-vb[DP DataView Samples#LDVFromQueryFindRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromqueryfindrows)]  
  
## <a name="aspnet"></a>ASP.NET  

 O ASP.NET tem um mecanismo de cachê que permite que você armazene os objetos que exigem recursos abrangentes de servidor criar na memória. Armazenar em cachê esses tipos de recursos pode melhorar significativamente o desempenho do seu aplicativo. Caching é implementado pela classe de <xref:System.Web.Caching.Cache> , com instâncias de cache que são particulares para cada aplicativo. Como criar um novo objeto de <xref:System.Data.DataView> pode ser recurso intensivo, você pode querer usar essa funcionalidade de cachê em aplicativos da Web para que <xref:System.Data.DataView> não tem que ser reconstruído todas as vezes na página da Web é atualizado.  
  
 No exemplo a seguir, <xref:System.Data.DataView> é armazenado em cachê de modo que os dados não precisem ser recorridos quando a página é atualizada.  
  
```vb  
If (Cache("ordersView") = Nothing) Then  
  
Dim dataSet As New DataSet()  
  
   FillDataSet(dataSet)  
  
   Dim orders As DataTable = dataSet.Tables("SalesOrderHeader")  
  
   Dim query = _  
                    From order In orders.AsEnumerable() _  
                    Where order.Field(Of Boolean)("OnlineOrderFlag") = True _  
                    Order By order.Field(Of Decimal)("TotalDue") _  
                    Select order  
  
   Dim view As DataView = query.AsDataView()  
  
   Cache.Insert("ordersView", view)  
  
End If  
  
Dim ordersView = CType(Cache("ordersView"), DataView)  
  
GridView1.DataSource = ordersView  
GridView1.DataBind()  
```  
  
```csharp  
if (Cache["ordersView"] == null)  
{  
   // Fill the DataSet.
   DataSet dataSet = FillDataSet();  
  
   DataTable orders = dataSet.Tables["SalesOrderHeader"];  
  
   EnumerableRowCollection<DataRow> query =  
                        from order in orders.AsEnumerable()  
                        where order.Field<bool>("OnlineOrderFlag") == true  
                        orderby order.Field<decimal>("TotalDue")  
                        select order;  
  
   DataView view = query.AsDataView();  
   Cache.Insert("ordersView", view);  
}  
  
DataView ordersView = (DataView)Cache["ordersView"];  
  
GridView1.DataSource = ordersView;  
GridView1.DataBind();  
```  
  
## <a name="see-also"></a>Consulte também

- [Associação e LINQ to DataSet de dados](data-binding-and-linq-to-dataset.md)
