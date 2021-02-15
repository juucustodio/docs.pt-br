---
description: 'Saiba mais sobre: gerando relações de conjunto de informações do esquema XML (XSD)'
title: Gerar relações de DataSet do esquema XML (XSD)
ms.date: 03/30/2017
ms.assetid: 1c9a1413-c0d2-4447-88ba-9a2b0cbc0aa8
ms.openlocfilehash: e18ae451085f536e7fe35053fadab35e30dbc225
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652452"
---
# <a name="generating-dataset-relations-from-xml-schema-xsd"></a>Gerar relações de DataSet do esquema XML (XSD)

Em um <xref:System.Data.DataSet> , você formam uma associação entre duas ou mais colunas criando uma relação pai-filho. Há três maneiras de representar uma relação de conjunto de um **DataSet** em um esquema XSD (linguagem de definição de esquema XML):  
  
- Especifique tipos complexos aninhados.  
  
- Use a anotação **MSDATA: relationship** .  
  
- Especifique um **xs: keyref** sem a anotação **MSDATA: ConstraintOnly** .  
  
## <a name="nested-complex-types"></a>Tipos complexos aninhados  

 Definições de tipo complexo aninhadas em um esquema indicam as relações pai-filho dos elementos. O fragmento de esquema XML a seguir mostra que **OrderDetail** é um elemento filho do elemento **Order** .  
  
```xml  
<xs:element name="Order">  
  <xs:complexType>  
     <xs:sequence>
       <xs:element name="OrderDetail" />  
           <xs:complexType>
           </xs:complexType>  
     </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 O processo de mapeamento de esquema XML cria tabelas no **conjunto** de um que correspondem aos tipos complexos aninhados no esquema. Ele também cria colunas adicionais que são usadas como **-** colunas filho pai para as tabelas geradas. Observe que essas **-** colunas filho pai especificam relações, que não são as mesmas que especificar restrições de chave primária/Foreign Key.  
  
## <a name="msdatarelationship-annotation"></a>MSDATA: anotação de relação  

 A anotação **MSDATA: relationship** permite especificar explicitamente as relações pai-filho entre os elementos no esquema que não estão aninhados. O exemplo a seguir mostra a estrutura do elemento **relationship** .  
  
```xml  
<msdata:Relationship name="CustOrderRelationship"
msdata:parent=""
msdata:child=""
msdata:parentkey=""
msdata:childkey="" />  
```  
  
 Os atributos da anotação **MSDATA: relationship** identificam os elementos envolvidos na relação pai-filho, bem como os elementos e atributos **ParentKey** e **ChildKey** envolvidos na relação. O processo de mapeamento usa essas informações para gerar tabelas no **conjunto** de dados e para criar a relação de chave primária/chave estrangeira entre essas tabelas.  
  
 Por exemplo, o seguinte fragmento de esquema especifica os elementos **Order** e **OrderDetail** no mesmo nível (não aninhado). O esquema especifica uma anotação **MSDATA: relationship** , que especifica a relação pai-filho entre esses dois elementos. Nesse caso, uma relação explícita deve ser especificada usando a anotação **MSDATA: relationship** .  
  
```xml  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
        <xs:element name="OrderDetail">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
       <xs:element name="Order">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
    </xs:choice>  
  </xs:complexType>  
</xs:element>  
   <xs:annotation>  
     <xs:appinfo>  
       <msdata:Relationship name="OrdOrdDetailRelation"  
          msdata:parent="Order"  
          msdata:child="OrderDetail"
          msdata:parentkey="OrderNumber"  
          msdata:childkey="OrderNo"/>  
     </xs:appinfo>  
  </xs:annotation>  
```  
  
 O processo de mapeamento usa o elemento **relationship** para criar uma relação pai-filho entre a coluna **OrderNumber** na tabela **Order** e a coluna **orderno** na tabela **OrderDetail** no **DataSet**. O processo de mapeamento especifica apenas a relação; Ele não especifica automaticamente nenhuma restrição nos valores dessas colunas, assim como as restrições de chave primária/chave estrangeira em bancos de dados relacionais.  
  
### <a name="in-this-section"></a>Nesta seção  

 [Mapear relações implícitas entre elementos de esquema aninhados](map-implicit-relations-between-nested-schema-elements.md)  
 Descreve as restrições e relações criadas implicitamente em um conjunto de um **DataSet** quando elementos aninhados são encontrados no esquema XML.  
  
 [Mapear relações especificadas para elementos aninhados](map-relations-specified-for-nested-elements.md)  
 Descreve como definir explicitamente relações em um **DataSet** para elementos aninhados no esquema XML.  
  
 [Especificar relações entre elementos sem nenhum aninhamento](specify-relations-between-elements-with-no-nesting.md)  
 Descreve como criar relações em um conjunto de um **DataSet** entre elementos de esquema XML que não estão aninhados.  
  
### <a name="related-sections"></a>Seções relacionadas  

 [Derivando a estrutura relacional do DataSet do esquema XML (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 Descreve a estrutura relacional, ou esquema, de um **conjunto** de dados criado a partir do esquema XSD (XML Schema Definition Language).  
  
 [Mapeamento de restrições de esquema XML (XSD) para restrições de DataSet](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Descreve os elementos de esquema XML usados para criar restrições de chave estrangeira e exclusivas em um **conjunto** de uma.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral do ADO.NET](../ado-net-overview.md)
