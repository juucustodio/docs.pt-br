---
description: 'Saiba mais sobre: especificar relações entre elementos sem aninhamento'
title: Especificar relações entre elementos sem nenhum aninhamento
ms.date: 03/30/2017
ms.assetid: e31325da-7691-4d33-acf4-99fccca67006
ms.openlocfilehash: 68f6edad0c282091529bf9182f5161d0808a47aa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651620"
---
# <a name="specify-relations-between-elements-with-no-nesting"></a>Especificar relações entre elementos sem nenhum aninhamento

Quando os elementos não são aninhados, nenhuma relação implícita é criada. No entanto, você pode especificar explicitamente as relações entre os elementos que não são aninhados usando a anotação **MSDATA: relationship** .  
  
 O exemplo a seguir mostra um esquema XML no qual a anotação **MSDATA: relationship** é especificada entre os elementos **Order** e **OrderDetail** , que não estão aninhados. A anotação **MSDATA: relationship** é especificada como o elemento filho do elemento **Schema** .  
  
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
           <xs:element name="OrderNo" type="xs:string" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNumber" type="xs:string" />  
           <xs:element name="EmpNumber" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  </xs:element>  
   <xs:annotation>  
     <xs:appinfo>  
       <msdata:Relationship name="OrdOrderDetailRelation"  
                            msdata:parent="Order"
                            msdata:child="OrderDetail"
                            msdata:parentkey="OrderNumber"
                            msdata:childkey="OrderNo"/>  
     </xs:appinfo>  
  </xs:annotation>  
</xs:schema>  
```  
  
 O processo de mapeamento de esquema XSD (linguagem de definição de esquema XML) cria um <xref:System.Data.DataSet> com tabelas **Order** e **OrderDetail** e uma relação especificada entre essas duas tabelas, como mostrado abaixo.  
  
```text  
RelationName: OrdOrderDetailRelation  
ParentTable: Order  
ParentColumns: OrderNumber
ChildTable: OrderDetail  
ChildColumns: OrderNo
Nested: False  
```  
  
## <a name="see-also"></a>Consulte também

- [Gerar relações de DataSet do esquema XML (XSD)](generating-dataset-relations-from-xml-schema-xsd.md)
- [Mapeamento de restrições de esquema XML (XSD) para restrições de DataSet](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
