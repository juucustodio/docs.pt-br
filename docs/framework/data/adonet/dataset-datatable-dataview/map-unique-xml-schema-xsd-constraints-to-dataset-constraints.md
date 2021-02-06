---
description: 'Saiba mais sobre: mapear restrições XSD (esquema XML exclusivo) para restrições de conjunto de informações'
title: Mapear de restrições de esquema XML (XSD) exclusivas para restrições de DataSet
ms.date: 03/30/2017
ms.assetid: 56da90bf-21d3-4d1a-8bb8-de908866b78d
ms.openlocfilehash: 41a6e5424d67b092e57ac61d6e34a1f285fb8d0c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651919"
---
# <a name="map-unique-xml-schema-xsd-constraints-to-dataset-constraints"></a>Mapear de restrições de esquema XML (XSD) exclusivas para restrições de DataSet

Em um esquema XSD (linguagem de definição de esquema XML), o elemento **exclusivo** especifica a restrição de exclusividade em um elemento ou atributo. No processo de tradução de um esquema XML em um esquema relacional, a restrição UNIQUE especificada em um elemento ou atributo no esquema XML é mapeada para uma restrição UNIQUE no <xref:System.Data.DataTable> no correspondente <xref:System.Data.DataSet> que é gerado.  
  
 A tabela a seguir descreve os atributos **MSDATA** que você pode especificar no elemento **Unique** .  
  
|Nome do atributo|Descrição|  
|--------------------|-----------------|  
|**MSDATA: ConstraintName**|Se esse atributo for especificado, seu valor será usado como o nome da restrição. Caso contrário, o atributo **Name** fornecerá o valor do nome da restrição.|  
|**MSDATA: PrimaryKey**|Se `PrimaryKey="true"` estiver presente no elemento **Unique** , uma restrição UNIQUE será criada com a propriedade **IsPrimaryKey** definida como **true**.|  
  
 O exemplo a seguir mostra um esquema XML que usa o elemento **exclusivo** para especificar uma restrição de exclusividade.  
  
```xml  
<xs:schema id="SampleDataSet"
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:integer"
           minOccurs="0"/>  
        <xs:element name="CompanyName" type="xs:string"
           minOccurs="0"/>  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
  
 <xs:element name="SampleDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:unique     msdata:ConstraintName="UCustID"     name="UniqueCustIDConstr" >       <xs:selector xpath=".//Customers" />       <xs:field xpath="CustomerID" />     </xs:unique>  
</xs:element>  
</xs:schema>  
```  
  
 O elemento **exclusivo** no esquema especifica que para todos os elementos **Customers** em uma instância de documento, o valor do elemento filho **CustomerID** deve ser exclusivo. Ao criar o **conjunto** de um, o processo de mapeamento lê esse esquema e gera a tabela a seguir:  
  
```text  
Customers (CustomerID, CompanyName, Phone)  
```  
  
 O processo de mapeamento também cria uma restrição UNIQUE na coluna **CustomerID** , conforme mostrado no **conjunto** de acordo a seguir. (Para simplificar, apenas as propriedades relevantes são mostradas.)  
  
```text  
      DataSetName: MyDataSet  
TableName: Customers  
  ColumnName: CustomerID  
      AllowDBNull: True  
      Unique: True  
  ConstraintName: UcustID       Type: UniqueConstraint  
      Table: Customers  
      Columns: CustomerID
      IsPrimaryKey: False  
```  
  
 No **conjunto** de um que é gerado, a propriedade **IsPrimaryKey** é definida como **false** para a restrição UNIQUE. A propriedade **Unique** na coluna indica que os valores de coluna **CustomerID** devem ser exclusivos (mas podem ser uma referência nula, conforme especificado pela propriedade **AllowDBNull** da coluna).  
  
 Se você modificar o esquema e definir o valor de atributo opcional **MSDATA: PrimaryKey** como **true**, a restrição UNIQUE será criada na tabela. A propriedade de coluna **AllowDBNull** é definida como **false** e a propriedade **IsPrimaryKey** da restrição definida como **true**, tornando a coluna **CustomerID** uma coluna de chave primária.  
  
 Você pode especificar uma restrição UNIQUE em uma combinação de elementos ou atributos no esquema XML. O exemplo a seguir demonstra como especificar que uma combinação de **CustomerID** e valores **CompanyName** deve ser exclusiva para todos os **clientes** em qualquer instância, adicionando outro elemento **xs: Field** no esquema.  
  
```xml  
      <xs:unique
         msdata:ConstraintName="SomeName"
         name="UniqueCustIDConstr" >
  <xs:selector xpath=".//Customers" />
  <xs:field xpath="CustomerID" />
  <xs:field xpath="CompanyName" />
</xs:unique>  
```  
  
 Essa é a restrição que é criada no **conjunto** de resultados resultante.  
  
```text  
ConstraintName: SomeName  
  Table: Customers  
  Columns: CustomerID CompanyName
  IsPrimaryKey: False  
```  
  
## <a name="see-also"></a>Consulte também

- [Mapeamento de restrições de esquema XML (XSD) para restrições de DataSet](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [Gerar relações de DataSet do esquema XML (XSD)](generating-dataset-relations-from-xml-schema-xsd.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
