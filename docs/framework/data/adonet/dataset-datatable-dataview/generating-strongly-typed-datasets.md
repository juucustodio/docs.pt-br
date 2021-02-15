---
description: 'Saiba mais sobre: gerando conjuntos de linhas com rigidez de tipos'
title: Gerando DataSets fortemente tipados
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 54333cbf-bb43-4314-a7d4-6dc1dd1c44b3
ms.openlocfilehash: c69aecc5a0a541c868dac3037c9dd0dbc3fe8383
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652426"
---
# <a name="generating-strongly-typed-datasets"></a>Gerando DataSets fortemente tipados

Dado um esquema XML que está em conformidade com o padrão XSD, você pode gerar um tipo fortemente tipado <xref:System.Data.DataSet> usando a ferramenta de XSD.exe fornecida com o SDK (Software Development Kit) do Windows.  
  
 (Para criar um XSD a partir de tabelas de banco de dados, consulte <xref:System.Data.DataSet.WriteXmlSchema%2A> ou [trabalhando com DataSets no Visual Studio](/visualstudio/data-tools/dataset-tools-in-visual-studio)).  
  
 O código a seguir mostra a sintaxe para gerar um conjunto de um **DataSet** usando essa ferramenta.  
  
```console  
xsd.exe /d /l:CS XSDSchemaFileName.xsd /eld /n:XSDSchema.Namespace  
```  
  
 Nessa sintaxe, a `/d` diretiva instrui a ferramenta a gerar um **conjunto** de um e `/l:` informa à ferramenta qual idioma usar (por exemplo, C# ou Visual Basic .net). A `/eld` diretiva opcional especifica que você pode usar LINQ to DataSet para consultar o conjunto de consulta gerado **.** Essa opção é usada quando a opção `/d` também está especificada. Para obter mais informações, consulte [consultando conjuntos de dados tipados](../querying-typed-datasets.md). A `/n:` diretiva opcional informa a ferramenta para também gerar um namespace para o **conjunto** de espaço chamado **XSDSchema. namespace**. A saída do comando é XSDSchemaFileName.cs, o que pode ser compilado e usado em um aplicativo ADO.NET. O código gerado pode ser compilado como uma biblioteca ou um módulo.  
  
 O código a seguir mostra a sintaxe para compilar o código gerado como uma biblioteca usando o compilador C# (csc.exe).  
  
```console  
csc.exe /t:library XSDSchemaFileName.cs /r:System.dll /r:System.Data.dll  
```  
  
 A política `/t:` diz à ferramenta para criar em uma biblioteca e as políticas `/r:` especificam as bibliotecas dependentes necessárias para compilar. A saída do comando é XSDSchemaFileName.dll, que pode ser passado para o compilador ao criar um aplicativo do ADO.NET com a política `/r:`.  
  
 O código a seguir mostra a sintaxe para acessar o namespace passado para XSD.exe em um aplicativo ADO.NET.  
  
```vb  
Imports XSDSchema.Namespace  
```  
  
```csharp  
using XSDSchema.Namespace;  
```  
  
 O exemplo de código a seguir usa um **DataSet** tipado chamado **CustomerDataSet** para carregar uma lista de clientes do banco de dados **Northwind** . Depois que os dados são carregados usando o método **Fill** , o exemplo percorre cada cliente na tabela **Customers** usando o objeto **CustomersRow** (**DataRow**) digitado. Isso fornece acesso direto à coluna **CustomerID** , em oposição ao por meio de **DataColumnCollection**.  
  
```vb  
Dim customers As CustomerDataSet= New CustomerDataSet()  
Dim adapter As SqlDataAdapter New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers;", _  
  "Data Source=(local);Integrated " & _  
  "Security=SSPI;Initial Catalog=Northwind")  
  
adapter.Fill(customers, "Customers")  
  
Dim customerRow As CustomerDataSet.CustomersRow  
For Each customerRow In customers.Customers  
  Console.WriteLine(customerRow.CustomerID)  
Next  
```  
  
```csharp  
CustomerDataSet customers = new CustomerDataSet();  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers;",  
  "Data Source=(local);Integrated " +  
  "Security=SSPI;Initial Catalog=Northwind");  
  
adapter.Fill(customers, "Customers");  
  
foreach(CustomerDataSet.CustomersRow customerRow in customers.Customers)  
  Console.WriteLine(customerRow.CustomerID);  
```  
  
 Este é o esquema XML usado para o exemplo:
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet" xmlns="" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataSet>
- [DataSets tipados](typed-datasets.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
