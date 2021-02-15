---
description: 'Saiba mais sobre: aplicando uma transformação XSLT a um conjunto de informações'
title: Aplicar uma transformação XSLT a um DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 09f2e4ee-1d08-4ba8-8936-83394fee319d
ms.openlocfilehash: c7fc25441091112f7fbb7e4c1f8dd210d8cd0c5d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99725110"
---
# <a name="applying-an-xslt-transform-to-a-dataset"></a>Aplicar uma transformação XSLT a um DataSet

O método **WriteXml** do <xref:System.Data.DataSet> permite que você grave o conteúdo de um **DataSet** como dados XML. Uma tarefa comum é transformar esse XML em outro formato usando transformações XSL (XSLT). No entanto, a sincronização de um **conjunto** de dados com um <xref:System.Xml.XmlDataDocument> permite que você aplique uma folha de estilos XSLT ao conteúdo de um **conjunto** de dados sem precisar primeiro gravar o conteúdo do **DataSet** como dado XML usando **WriteXml**.  
  
 O exemplo a seguir popula um **conjunto** de um DataSet com tabelas e relações, sincroniza o **conjunto** de os com um **XmlDataDocument** e grava uma parte do **conjunto** de um arquivo HTML usando uma folha de estilos XSLT. Veja a seguir o conteúdo da folha de estilos XSLT:
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">  
  
<xsl:template match="CustomerOrders">  
  <HTML>  
  <STYLE>  
  BODY {font-family:verdana;font-size:9pt}  
  TD   {font-size:8pt}  
  </STYLE>  
    <BODY>  
    <TABLE BORDER="1">  
      <xsl:apply-templates select="Customers"/>  
    </TABLE>  
    </BODY>  
  </HTML>  
</xsl:template>  
  
<xsl:template match="Customers">  
    <TR><TD>  
      <xsl:value-of select="ContactName"/>, <xsl:value-of select="Phone"/><BR/>  
    </TD></TR>  
      <xsl:apply-templates select="Orders"/>  
</xsl:template>  
  
<xsl:template match="Orders">  
  <TABLE BORDER="1">  
    <TR><TD valign="top"><B>Order:</B></TD><TD valign="top"><xsl:value-of select="OrderID"/></TD></TR>  
    <TR><TD valign="top"><B>Date:</B></TD><TD valign="top"><xsl:value-of select="OrderDate"/></TD></TR>  
    <TR><TD valign="top"><B>Ship To:</B></TD>  
        <TD valign="top"><xsl:value-of select="ShipName"/><BR/>  
        <xsl:value-of select="ShipAddress"/><BR/>  
        <xsl:value-of select="ShipCity"/>, <xsl:value-of select="ShipRegion"/>  <xsl:value-of select="ShipPostalCode"/><BR/>  
        <xsl:value-of select="ShipCountry"/></TD></TR>  
  </TABLE>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
 O código a seguir preenche o **DataSet** e aplica a folha de estilos XSLT.  
  
> [!NOTE]
> Se você estiver aplicando uma folha de estilos XSLT a um **conjunto** de um que contém relações, você obterá o melhor desempenho se definir a propriedade **aninhada** de <xref:System.Data.DataRelation> como **true** para cada relação aninhada. Isso permite que você use folhas de estilo XSLT que implementam o processamento de cima para baixo natural para navegar pela hierarquia e transformar os dados, em oposição ao uso de eixos de local XPath com uso intensivo de desempenho (por exemplo, irmão precedentes e o irmão seguinte em expressões de teste de nó de folha de estilo) para navegar por ele. Para obter mais informações sobre relações aninhadas, consulte [aninhando DataRelations](nesting-datarelations.md).  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Customers", connection)  
customerAdapter.Fill(dataSet, "Customers")  
  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Orders", connection)  
orderAdapter.Fill(dataSet, "Orders")  
  
connection.Close()  
  
dataSet.Relations.Add("CustOrders", _  
dataSet.Tables("Customers").Columns("CustomerID"), _  
dataSet.Tables("Orders").Columns("CustomerID")).Nested = true  
  
Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)
  
Dim xslTran As XslTransform = New XslTransform  
xslTran.Load("transform.xsl")  
  
Dim writer As XmlTextWriter = New XmlTextWriter( _  
  "xslt_output.html", System.Text.Encoding.UTF8)  
  
xslTran.Transform(xmlDoc, Nothing, writer)  
writer.Close()  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
connection.Open();  
  
DataSet custDS = new DataSet("CustomerDataSet");  
  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT * FROM Customers", connection);  
customerAdapter.Fill(custDS, "Customers");  
  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT * FROM Orders", connection);  
orderAdapter.Fill(custDS, "Orders");  
  
connection.Close();  
  
custDS.Relations.Add("CustOrders",  
  custDS.Tables["Customers"].Columns["CustomerID"],  
                     custDS.Tables["Orders"].Columns["CustomerID"]).Nested = true;  
  
XmlDataDocument xmlDoc = new XmlDataDocument(custDS);
  
XslTransform xslTran = new XslTransform();  
xslTran.Load("transform.xsl");  
  
XmlTextWriter writer = new XmlTextWriter("xslt_output.html",
  System.Text.Encoding.UTF8);  
  
xslTran.Transform(xmlDoc, null, writer);  
writer.Close();  
```  
  
## <a name="see-also"></a>Consulte também

- [Sincronização de DataSet e XmlDataDocument](dataset-and-xmldatadocument-synchronization.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
