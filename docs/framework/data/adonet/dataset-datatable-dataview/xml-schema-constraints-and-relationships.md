---
description: 'Saiba mais sobre: restrições e relações de esquema XML'
title: Relações e restrições de esquema XML
ms.date: 03/30/2017
ms.assetid: 165bc2bc-60a1-40e0-9b89-7c68ef979079
ms.openlocfilehash: c7847691537c4b754abcbacdeb367b1d92365ef3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651308"
---
# <a name="xml-schema-constraints-and-relationships"></a>Relações e restrições de esquema XML

Em um esquema XSD (linguagem de definição de esquema XML), você pode especificar restrições (restrições UNIQUE, Key e keyref) e relações (usando a anotação **MSDATA: relationship** ). Este tópico explica como as restrições e as relações especificadas em um esquema XML são interpretadas para gerar o <xref:System.Data.DataSet> .  
  
 Em geral, em um esquema XML, você especifica a anotação **MSDATA: relationship** se você quiser gerar somente relações no **conjunto** de uma. Para obter mais informações, consulte [gerando relações de conjunto de dados do esquema XML (XSD)](generating-dataset-relations-from-xml-schema-xsd.md). Você especifica restrições (Unique, Key e keyref) se desejar gerar restrições no **conjunto** de testes. Observe que as restrições Key e keyref também são usadas para gerar relações, conforme explicado posteriormente neste tópico.  
  
## <a name="generating-a-relationship-from-key-and-keyref-constraints"></a>Gerando uma relação de restrições de chave e keyref  

 Em vez de especificar a anotação **MSDATA: relationship** , você pode especificar as restrições de Key e keyref, que são usadas durante o processo de mapeamento de esquema XML para gerar não apenas as restrições, mas também a relação no **DataSet**. No entanto, se você especificar `msdata:ConstraintOnly="true"` no elemento **keyref** , o **conjunto** de testes incluirá apenas as restrições e não incluirá a relação.  
  
 O exemplo a seguir mostra um esquema XML que inclui elementos **Order** e **OrderDetail** , que não estão aninhados. O esquema também especifica as restrições de chave e keyref.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 O **conjunto** de os que é gerado durante o processo de mapeamento de esquema XML inclui as tabelas **Order** e **OrderDetail** . Além disso, o **conjunto** de testes inclui relações e restrições. O exemplo a seguir mostra essas relações e restrições. Observe que o esquema não especifica a anotação **MSDATA: relationship** ; em vez disso, as restrições Key e keyref são usadas para gerar a relação.  
  
```text
....ConstraintName: OrderNumberKey  
....Type: UniqueConstraint  
....Table: Order  
....Columns: OrderNumber  
....IsPrimaryKey: False  
  
....ConstraintName: OrderNoRef  
....Type: ForeignKeyConstraint  
....Table: OrderDetail  
....Columns: OrderNo  
....RelatedTable: Order  
....RelatedColumns: OrderNumber  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
```  
  
 No exemplo de esquema anterior, os elementos **Order** e **OrderDetail** não são aninhados. No exemplo de esquema a seguir, esses elementos são aninhados. No entanto, nenhuma **MSDATA:** a anotação de relação foi especificada; Portanto, uma relação implícita é assumida. Para obter mais informações, consulte [mapear relações implícitas entre elementos de esquema aninhados](map-implicit-relations-between-nested-schema-elements.md). O esquema também especifica as restrições de chave e keyref.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:integer" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 O **conjunto** de resultados resultante do processo de mapeamento de esquema XML inclui duas tabelas:  
  
```text  
Order(OrderNumber, EmpNumber, Order_Id)  
OrderDetail(OrderNumber, ItemNumber, Order_Id)  
```  
  
 O **conjunto** de e também inclui as duas relações (uma com base na anotação **MSDATA: relationship** e a outra com base nas restrições Key e keyref) e várias restrições. O exemplo a seguir mostra as relações e restrições.  
  
```text
..RelationName: Order_OrderDetail  
..ParentTable: Order  
..ParentColumns: Order_Id  
..ChildTable: OrderDetail  
..ChildColumns: Order_Id  
..ParentKeyConstraint: Constraint1  
..ChildKeyConstraint: Order_OrderDetail  
..Nested: True  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
  
..ConstraintName: OrderNumberKey  
..Type: UniqueConstraint  
..Table: Order  
..Columns: OrderNumber  
..IsPrimaryKey: False  
  
..ConstraintName: Constraint1  
..Type: UniqueConstraint  
..Table: Order  
..Columns: Order_Id  
..IsPrimaryKey: True  
  
..ConstraintName: Order_OrderDetail  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: Order_Id  
..RelatedTable: Order  
..RelatedColumns: Order_Id  
  
..ConstraintName: OrderNoRef  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: OrderNo  
..RelatedTable: Order  
..RelatedColumns: OrderNumber  
```  
  
 Se uma restrição keyref que faz referência a uma tabela aninhada contiver a anotação **MSDATA: Isnestd = "true"** , o **conjunto** de um criará uma única relação aninhada com base na restrição keyref e a restrição UNIQUE/KEY relacionada.  
  
## <a name="see-also"></a>Consulte também

- [Derivando a estrutura relacional do DataSet do esquema XML (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
