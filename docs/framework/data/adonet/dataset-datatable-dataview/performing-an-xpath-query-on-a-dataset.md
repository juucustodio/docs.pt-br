---
description: 'Saiba mais sobre: executando uma consulta XPath em um conjunto de informações'
title: Executar uma consulta XPath em um DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7e828566-fffe-4d38-abb2-4d68fd73f663
ms.openlocfilehash: 9febcc545f86f048b2d693f8aa6558a1b7883a60
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651711"
---
# <a name="performing-an-xpath-query-on-a-dataset"></a>Executar uma consulta XPath em um DataSet

A relação entre um sincronizado <xref:System.Data.DataSet> e <xref:System.Xml.XmlDataDocument> permite que você faça uso de serviços XML, como a consulta XPath, que acessa o **XmlDataDocument** e pode executar determinadas funcionalidades de forma mais conveniente do que acessar o **conjunto** de informações diretamente. Por exemplo, em vez de usar o método **Select** de <xref:System.Data.DataTable> a para navegar em relações com outras tabelas em um **conjunto** de um DataSet, você pode executar uma consulta XPath em um **XmlDataDocument** que é sincronizado com o **DataSet**, para obter uma lista de elementos XML na forma de um <xref:System.Xml.XmlNodeList> . Os nós na **XmlNodeList**, Cast como <xref:System.Xml.XmlElement> Nodes, podem ser passados para o método **GetRowFromElement** do **XmlDataDocument**, para retornar <xref:System.Data.DataRow> referências correspondentes às linhas da tabela no **conjunto** de registros sincronizado.  
  
 Por exemplo, o exemplo de código a seguir executa uma consulta XPath "neto". O **DataSet** é preenchido com três tabelas: **Customers**, **Orders** e **OrderDetails**. No exemplo, uma relação pai-filho é criada primeiro entre as tabelas **Customers** e **Orders** e entre as tabelas **Orders** e **OrderDetails** . Em seguida, uma consulta XPath é executada para retornar um XmlNodeList **de nós** de **clientes** em que um nó neto **OrderDetails** tem um nó **ProductID** com o valor de 43. Em essência, o exemplo está usando a consulta XPath para determinar quais clientes solicitaram o produto com o **ProductID** de 43.  
  
```vb  
' Assumes that connection is a valid SqlConnection.  
connection.Open()  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Customers", connection)  
customerAdapter.Fill(dataSet, "Customers")  
  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Orders", connection)  
orderAdapter.Fill(dataSet, "Orders")  
  
Dim detailAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM [Order Details]", connection)  
detailAdapter.Fill(dataSet, "OrderDetails")  
  
connection.Close()  
  
dataSet.Relations.Add("CustOrders", _  
dataSet.Tables("Customers").Columns("CustomerID"), _  
dataSet.Tables("Orders").Columns("CustomerID")).Nested = true  
  
dataSet.Relations.Add("OrderDetail", _  
  dataSet.Tables("Orders").Columns("OrderID"), _  
dataSet.Tables("OrderDetails").Columns("OrderID"), false).Nested = true  
  
Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)
  
Dim nodeList As XmlNodeList = xmlDoc.DocumentElement.SelectNodes( _  
  "descendant::Customers[*/OrderDetails/ProductID=43]")  
  
Dim dataRow As DataRow  
Dim xmlNode As XmlNode  
  
For Each xmlNode In nodeList  
  dataRow = xmlDoc.GetRowFromElement(CType(xmlNode, XmlElement))  
  
  If Not dataRow Is Nothing then Console.WriteLine(xmlRow(0).ToString())  
Next  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection.  
connection.Open();  
  
DataSet dataSet = new DataSet("CustomerOrders");  
  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT * FROM Customers", connection);  
customerAdapter.Fill(dataSet, "Customers");  
  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT * FROM Orders", connection);  
orderAdapter.Fill(dataSet, "Orders");  
  
SqlDataAdapter detailAdapter = new SqlDataAdapter(  
  "SELECT * FROM [Order Details]", connection);  
detailAdapter.Fill(dataSet, "OrderDetails");  
  
connection.Close();  
  
dataSet.Relations.Add("CustOrders",  
  dataSet.Tables["Customers"].Columns["CustomerID"],  
 dataSet.Tables["Orders"].Columns["CustomerID"]).Nested = true;  
  
dataSet.Relations.Add("OrderDetail",  
  dataSet.Tables["Orders"].Columns["OrderID"],  
  dataSet.Tables["OrderDetails"].Columns["OrderID"],
  false).Nested = true;  
  
XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);
  
XmlNodeList nodeList = xmlDoc.DocumentElement.SelectNodes(  
  "descendant::Customers[*/OrderDetails/ProductID=43]");  
  
DataRow dataRow;  
foreach (XmlNode xmlNode in nodeList)  
{  
  dataRow = xmlDoc.GetRowFromElement((XmlElement)xmlNode);  
  if (dataRow != null)  
    Console.WriteLine(dataRow[0]);  
}  
```  
  
## <a name="see-also"></a>Consulte também

- [Sincronização de DataSet e XmlDataDocument](dataset-and-xmldatadocument-synchronization.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
