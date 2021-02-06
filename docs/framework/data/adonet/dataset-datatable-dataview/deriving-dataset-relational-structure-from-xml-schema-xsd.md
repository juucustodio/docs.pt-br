---
description: 'Saiba mais sobre: derivar a estrutura relacional do conjunto de dados do esquema XML (XSD)'
title: Derivando a estrutura relacional do DataSet do esquema XML (XSD)
ms.date: 03/30/2017
ms.assetid: 8f6cd04d-6197-4bc4-9096-8c51c7e4acae
ms.openlocfilehash: c2d2dc8ab9c8a1cf77c79fbde38a06de6f120c82
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652517"
---
# <a name="deriving-dataset-relational-structure-from-xml-schema-xsd"></a>Derivando a estrutura relacional do DataSet do esquema XML (XSD)

Esta seção fornece uma visão geral de como o esquema relacional de um `DataSet` é compilado a partir de um documento de esquema XSD (linguagem de definição de esquema XML). Em geral, para cada `complexType` elemento filho de um elemento de esquema, uma tabela é gerada no `DataSet` . A estrutura da tabela é determinada pela definição do tipo complexo. As tabelas são criadas no `DataSet` para elementos de nível superior no esquema. No entanto, uma tabela é criada somente para um elemento de nível superior `complexType` quando o `complexType` elemento é aninhado dentro de outro `complexType` elemento; nesse caso, o elemento aninhado `complexType` é mapeado para um `DataTable` dentro do `DataSet` .  
  
 Para obter mais informações sobre o XSD, consulte o esquema XML do World Wide Web Consortium (W3C) [parte 0: recomendação do primer](https://www.w3.org/TR/xmlschema-0/), o [esquema XML parte 1: recomendação de estruturas](https://www.w3.org/TR/xmlschema-1/)e o [esquema XML parte 2: recomendação de tipos](https://www.w3.org/TR/xmlschema-2/)de dados.  
  
 O exemplo a seguir demonstra um esquema XML em que `customers` é o elemento filho do `MyDataSet` elemento, que é um elemento **DataSet** .  
  
```xml  
<xs:schema id="SomeID"
            xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element name="customers" >
           <xs:complexType >  
             <xs:sequence>  
               <xs:element name="CustomerID" type="xs:integer"
                            minOccurs="0" />  
               <xs:element name="CompanyName" type="xs:string"
                            minOccurs="0" />  
               <xs:element name="Phone" type="xs:string" />  
             </xs:sequence>  
           </xs:complexType>  
          </xs:element>  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 No exemplo anterior, o elemento `customers` é um elemento de tipo complexo. Portanto, o definição de tipo complexo é analisada, e o processo de mapeamento cria a tabela a seguir.  
  
```text  
Customers (CustomerID, CompanyName, Phone)  
```  
  
 O tipo de dados de cada coluna na tabela é derivado do tipo do Esquema XML do elemento ou atributo correspondente especificado.  
  
> [!NOTE]
> Se o elemento `customers` for de um tipo de dados de esquema XML simples, como **Integer**, nenhuma tabela será gerada. As tabelas são criadas apenas para os elementos de nível superior que são tipos complexos.  
  
 No esquema XML a seguir, o elemento **Schema** tem dois elementos filho `InStateCustomers` e `OutOfStateCustomers` .  
  
```xml  
<xs:schema id="SomeID"
            xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="InStateCustomers" type="customerType" />  
   <xs:element name="OutOfStateCustomers" type="customerType" />  
    <xs:complexType name="customerType" >  
  
     </xs:complexType>  
  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element ref="customers" />  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 Os elementos filho `InStateCustomers` e `OutOfStateCustomers` são ambos elementos de tipo complexo (`customerType`). Portanto, o processo de mapeamento gera as duas tabelas idênticas a seguir no `DataSet` .  
  
```text  
InStateCustomers (CustomerID, CompanyName, Phone)  
OutOfStateCustomers (CustomerID, CompanyName, Phone)  
```  
  
## <a name="in-this-section"></a>Nesta seção  

 [Mapeamento de restrições de esquema XML (XSD) para restrições de DataSet](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Descreve os elementos de esquema XML usados para criar restrições de chave estrangeira e exclusivas em um `DataSet` .  
  
 [Gerar relações de DataSet do esquema XML (XSD)](generating-dataset-relations-from-xml-schema-xsd.md)  
 Descreve os elementos de esquema XML usados para criar relações entre colunas de tabela em um `DataSet` .  
  
 [Relações e restrições de esquema XML](xml-schema-constraints-and-relationships.md)  
 Descreve como as relações são criadas implicitamente ao usar elementos de esquema XML para criar restrições em um `DataSet` .  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Usando XML em um DataSet](using-xml-in-a-dataset.md)  
 Descreve como carregar e manter a estrutura relacional e os dados em um `DataSet` como dados XML.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral do ADO.NET](../ado-net-overview.md)
