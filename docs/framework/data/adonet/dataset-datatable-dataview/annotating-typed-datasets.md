---
description: 'Saiba mais sobre: anotando conjuntos de linhas tipados'
title: Anotando DataSets tipados
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f82aaa62-321e-4c8a-b51b-9d1114700170
ms.openlocfilehash: 6f5838e94d88fd6c9b3a1991d4c8023d5892b784
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739697"
---
# <a name="annotating-typed-datasets"></a>Anotando DataSets tipados

As anotações permitem que você modifique os nomes dos elementos em seu <xref:System.Data.DataSet> tipado sem modificar o esquema subjacente. Modificar os nomes dos elementos em seu esquema subjacente faria com que o **conjunto** de dados digitado se refira a objetos que não existem na fonte de dado, além de perder uma referência aos objetos que existem na fonte de dados.  
  
 Usando anotações, você pode personalizar os nomes de objetos no **conjunto** de informações tipado com nomes mais significativos, tornando o código mais legível e o **conjunto** de informações tipado mais fácil para os clientes usarem, deixando o esquema subjacente intacto. Por exemplo, o seguinte elemento de esquema para a tabela **Customers** do banco de dados **Northwind** resultaria em um nome de objeto **DataRow** de **CustomersRow** e um <xref:System.Data.DataRowCollection> **Customers**.  
  
```xml  
<xs:element name="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 Um nome de **DataRowCollection** de **clientes** é significativo no código do cliente, mas um nome de **DataRow** de **CustomersRow** é enganoso porque é um único objeto. Além disso, em cenários comuns, o objeto seria referenciado sem o identificador de **linha** e, em vez disso, seria simplesmente chamado de objeto **Customer** . A solução é anotar o esquema e identificar novos nomes para os objetos **DataRow** e **DataRowCollection** . Veja a seguir a versão anotada do esquema anterior.  
  
```xml  
<xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 Especificar um valor **tipado** de **Customer** resultará em um nome de objeto **DataRow** de **Customer**. A especificação de um valor **typedPlural** de **clientes** preserva o nome de **DataRowCollection** dos **clientes**.  
  
 A tabela a seguir mostra as anotações disponíveis para uso.  
  
|Annotation|Descrição|  
|----------------|-----------------|  
|**typedName**|Nome do objeto.|  
|**typedPlural**|Nome de uma coleção de objetos.|  
|**typedParent**|Nome do objeto quando chamado em uma relação de pai.|  
|**typedChildren**|Nome do método para retornar objetos de uma relação filho.|  
|**nullValue**|Valor se o valor subjacente for **DBNull**. Consulte a tabela a seguir para anotações de **NullValue** . O padrão é **_throw**.|  
  
 A tabela a seguir mostra os valores que podem ser especificados para a anotação **NullValue** .  
  
|Valor nullValue|Descrição|  
|---------------------|-----------------|  
|*Valor de substituição*|Especifique um valor a ser retornado. O valor retornado deve corresponder ao tipo de elemento. Por exemplo, use `nullValue="0"` para retornar 0 para campos de inteiro nulos.|  
|**_throw**|Gera uma exceção. Este é o padrão.|  
|**_null**|Retorna uma referência nula ou gera uma exceção se um tipo primitivo for localizado.|  
|**_empty**|Para cadeias de **caracteres, retorna String. Empty**; caso contrário, retorna um objeto criado a partir de um construtor vazio. Se um tipo primitivo for encontrado, gera uma exceção.|  
  
 A tabela a seguir mostra valores padrão para objetos em um **DataSet** tipado e as anotações disponíveis.  
  
|Objeto/método/evento|Padrão|Annotation|  
|---------------------------|-------------|----------------|  
|**DataTable**|TableNameDataTable|typedPlural|  
|**DataTable** Maneiras|NewTableNameRow<br /><br /> AddTableNameRow<br /><br /> DeleteTableNameRow|typedName|  
|**DataRowCollection**|TableName|typedPlural|  
|**DataRow**|TableNameRow|typedName|  
|**DataColumn**|DataTable.ColumnNameColumn<br /><br /> DataRow.ColumnName|typedName|  
|**Propriedade**|PropertyName|typedName|  
|**Filho** Essa|GetChildTableNameRows|typedChildren|  
|**Pai** Essa|TableNameRow|typedParent|  
|**Conjunto** de LostFocus|TableNameRowChangeEvent<br /><br /> TableNameRowChangeEventHandler|typedName|  
  
 Para usar anotações de **DataSet** tipado, você deve incluir a seguinte referência **xmlns** em seu esquema de linguagem de definição de esquema XML (XSD). Para criar um XSD a partir de tabelas de banco de dados, consulte <xref:System.Data.DataSet.WriteXmlSchema%2A> ou [trabalhando com DataSets no Visual Studio](/visualstudio/data-tools/dataset-tools-in-visual-studio).  
  
```xml  
xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
```  
  
 Veja a seguir um esquema anotado de exemplo que expõe a tabela **Customers** do banco de dados **Northwind** com uma relação à tabela **Orders** incluída.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet"
      xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
      xmlns=""
      xmlns:xs="http://www.w3.org/2001/XMLSchema"
      xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID" type="xs:string" minOccurs="0" />  
              <xs:element name="CompanyName"  
codegen:typedName="CompanyName" type="xs:string" minOccurs="0" />  
              <xs:element name="Phone" codegen:typedName="Phone" codegen:nullValue="" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
        <xs:element name="Orders" codegen:typedName="Order" codegen:typedPlural="Orders">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="OrderID" codegen:typedName="OrderID"  
type="xs:int" minOccurs="0" />  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID"                  codegen:nullValue="" type="xs:string" minOccurs="0" />  
              <xs:element name="EmployeeID"  
codegen:typedName="EmployeeID" codegen:nullValue="0"
type="xs:int" minOccurs="0" />  
              <xs:element name="OrderAdapter"  
codegen:typedName="OrderAdapter" codegen:nullValue="1980-01-01T00:00:00"
type="xs:dateTime" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
    <xs:unique name="Constraint1">  
      <xs:selector xpath=".//Customers" />  
      <xs:field xpath="CustomerID" />  
    </xs:unique>  
    <xs:keyref name="CustOrders" refer="Constraint1"  
codegen:typedParent="Customer" codegen:typedChildren="GetOrders">  
      <xs:selector xpath=".//Orders" />  
      <xs:field xpath="CustomerID" />  
    </xs:keyref>  
  </xs:element>  
</xs:schema>  
```  
  
 O exemplo de código a seguir usa um **conjunto** de tipos fortemente tipado criado a partir do esquema de exemplo. Ele usa um <xref:System.Data.SqlClient.SqlDataAdapter> para popular a tabela **Customers** e outra <xref:System.Data.SqlClient.SqlDataAdapter> para popular a tabela **Orders** . O **DataSet** com rigidez de tipos define os **DataRelations**.  
  
```vb  
' Assumes a valid SqlConnection object named connection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT CustomerID, CompanyName, Phone FROM Customers", &  
    connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders", &  
    connection)  
  
' Populate a strongly typed DataSet.  
connection.Open()  
Dim customers As CustomerDataSet = New CustomerDataSet()  
customerAdapter.Fill(customers, "Customers")  
orderAdapter.Fill(customers, "Orders")  
connection.Close()  
  
' Add a strongly typed event.  
AddHandler customers.Customers.CustomerChanged, &  
    New CustomerDataSet.CustomerChangeEventHandler( _  
    AddressOf OnCustomerChanged)  
  
' Add a strongly typed DataRow.  
Dim newCustomer As CustomerDataSet.Customer = _  
    customers.Customers.NewCustomer()  
newCustomer.CustomerID = "NEW01"  
newCustomer.CompanyName = "My New Company"  
customers.Customers.AddCustomer(newCustomer)  
  
' Navigate the child relation.  
Dim customer As CustomerDataSet.Customer  
Dim order As CustomerDataSet.Order  
  
For Each customer In customers.Customers  
  Console.WriteLine(customer.CustomerID)  
  For Each order In customer.GetOrders()  
    Console.WriteLine(vbTab & order.OrderID)  
  Next  
Next  
  
Private Shared Sub OnCustomerChanged( _  
    sender As Object, e As CustomerDataSet.CustomerChangeEvent)  
  
End Sub  
```  
  
```csharp  
// Assumes a valid SqlConnection object named connection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
    "SELECT CustomerID, CompanyName, Phone FROM Customers",  
    connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders",
    connection);  
  
// Populate a strongly typed DataSet.  
connection.Open();  
CustomerDataSet customers = new CustomerDataSet();  
customerAdapter.Fill(customers, "Customers");  
orderAdapter.Fill(customers, "Orders");  
connection.Close();  
  
// Add a strongly typed event.  
customers.Customers.CustomerChanged += new
  CustomerDataSet.CustomerChangeEventHandler(OnCustomerChanged);  
  
// Add a strongly typed DataRow.  
CustomerDataSet.Customer newCustomer =
    customers.Customers.NewCustomer();  
newCustomer.CustomerID = "NEW01";  
newCustomer.CompanyName = "My New Company";  
customers.Customers.AddCustomer(newCustomer);  
  
// Navigate the child relation.  
foreach(CustomerDataSet.Customer customer in customers.Customers)  
{  
  Console.WriteLine(customer.CustomerID);  
  foreach(CustomerDataSet.Order order in customer.GetOrders())  
    Console.WriteLine("\t" + order.OrderID);  
}  
  
protected static void OnCustomerChanged(object sender, CustomerDataSet.CustomerChangeEvent e)  
    {  
  
    }  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataSet>
- [DataSets tipados](typed-datasets.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
