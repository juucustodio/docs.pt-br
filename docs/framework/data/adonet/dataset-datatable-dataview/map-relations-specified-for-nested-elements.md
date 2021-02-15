---
description: 'Saiba mais sobre: mapear relações especificadas para elementos aninhados'
title: Mapear relações especificadas para elementos aninhados
ms.date: 03/30/2017
ms.assetid: 24a2d3e5-4af7-4f9a-ab7a-fe6684c9e4fe
ms.openlocfilehash: a625ad5bfd590794d0362a991dc22f756f043f2a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651932"
---
# <a name="map-relations-specified-for-nested-elements"></a>Mapear relações especificadas para elementos aninhados

Um esquema pode incluir uma anotação **MSDATA: relationship** para especificar explicitamente o mapeamento entre quaisquer dois elementos no esquema. Os dois elementos especificados em **MSDATA: relationship** podem ser aninhados no esquema, mas não precisam ser. O processo de mapeamento usa a **relação MSDATA:** no esquema para gerar a relação de chave primária/chave estrangeira entre as duas colunas.  
  
 O exemplo a seguir mostra um esquema XML no qual o elemento **OrderDetail** é um elemento filho de **Order**. A **relação MSDATA:** identifica essa relação pai-filho e especifica que a coluna **OrderNumber** da tabela de **ordem** resultante está relacionada à coluna **orderno** da tabela **OrderDetail** resultante.  
  
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
       <xs:element name="OrderNumber" type="xs:string" />  
       <xs:element name="EmpNumber" type="xs:string" />  
       <xs:element name="OrderDetail">  
          <xs:annotation>  
           <xs:appinfo>  
            <msdata:Relationship name="OrdODRelation"
                                msdata:parent="Order"
                                msdata:child="OrderDetail"
                                msdata:parentkey="OrderNumber"
                                msdata:childkey="OrderNo"/>  
           </xs:appinfo>  
          </xs:annotation>  
          <xs:complexType>  
            <xs:sequence>  
             <xs:element name="OrderNo" type="xs:string" />  
             <xs:element name="ItemNo" type="xs:string" />  
            </xs:sequence>  
         </xs:complexType>  
       </xs:element>  
     </xs:sequence>  
    </xs:complexType>  
   </xs:element>  
  </xs:choice>  
 </xs:complexType>  
</xs:element>  
</xs:schema>  
```  
  
 O processo de mapeamento de esquema XML cria o seguinte no <xref:System.Data.DataSet> :  
  
- Uma **ordem** e uma tabela **OrderDetail** .  
  
    ```text  
    Order(OrderNumber, EmpNumber)  
    OrderDetail(OrderNo, ItemNo)  
    ```  
  
- Uma relação entre as tabelas **Order** e **OrderDetail** . A propriedade **aninhada** para essa relação é definida como **true** porque os elementos **Order** e **OrderDetail** estão aninhados no esquema.  
  
    ```text  
    ParentTable: Order  
    ParentColumns: OrderNumber
    ChildTable: OrderDetail  
    ChildColumns: OrderNo
    RelationName: OrdODRelation  
    Nested: True  
    ```  
  
 O processo de mapeamento não cria nenhuma restrição.  
  
## <a name="see-also"></a>Consulte também

- [Gerar relações de DataSet do esquema XML (XSD)](generating-dataset-relations-from-xml-schema-xsd.md)
- [Mapeamento de restrições de esquema XML (XSD) para restrições de DataSet](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
