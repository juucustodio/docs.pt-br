---
description: 'Saiba mais sobre: gravando informações de esquema de conjunto de dados como XSD'
title: Gravar informações de esquema de DataSet como XSD
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4e530831-695e-49ff-8f0b-e5b0c526b8eb
ms.openlocfilehash: e05188c74ca21e73ee5151da817e143102640a13
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651347"
---
# <a name="writing-dataset-schema-information-as-xsd"></a>Gravar informações de esquema de DataSet como XSD

Você pode gravar o esquema de um <xref:System.Data.DataSet> esquema XSD (linguagem de definição de esquema XML), para que você possa transportá-lo, com ou sem dados relacionados, em um documento XML. O esquema XML pode ser gravado em um arquivo, um fluxo, uma <xref:System.Xml.XmlWriter> ou uma cadeia de caracteres; ele é útil para gerar um **conjunto** de um DataSet com rigidez de tipos. Para obter mais informações sobre objetos de **conjunto** de dados com rigidez de tipos, consulte [datasets tipados](typed-datasets.md).  
  
 Você pode especificar como uma coluna de uma tabela é representada no esquema XML usando a propriedade **ColumnMapping** do <xref:System.Data.DataColumn> objeto. Para obter mais informações, consulte "Mapeando colunas para elementos XML, atributos e texto" na [escrita do conteúdo do conjunto de dados como dado XML](writing-dataset-contents-as-xml-data.md).  
  
 Para gravar o esquema de um **conjunto** de uma como esquema XML, em um arquivo, fluxo ou **XmlWriter**, use o método **WriteXmlSchema** do **conjunto** de um. **WriteXmlSchema** Obtém um parâmetro que especifica o destino do esquema XML resultante. Os exemplos de código a seguir demonstram como gravar o esquema XML de um **conjunto** de um em um arquivo, passando uma cadeia de caracteres contendo um nome de arquivo e um <xref:System.IO.StreamWriter> objeto.  
  
```vb  
dataSet.WriteXmlSchema("Customers.xsd")  
```  
  
```csharp  
dataSet.WriteXmlSchema("Customers.xsd");  
```  
  
```vb  
Dim writer As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xsd")  
dataSet.WriteXmlSchema(writer)  
writer.Close()  
```  
  
```csharp  
System.IO.StreamWriter writer = new System.IO.StreamWriter("Customers.xsd");  
dataSet.WriteXmlSchema(writer);  
writer.Close();  
```  
  
 Para obter o esquema de um **conjunto** de um e gravá-lo como uma cadeia de caracteres de esquema XML, use o método **GetXmlSchema** , conforme mostrado no exemplo a seguir.  
  
```vb  
Dim schemaString As String = dataSet.GetXmlSchema()  
```  
  
```csharp  
string schemaString = dataSet.GetXmlSchema();  
```  
  
## <a name="see-also"></a>Consulte também

- [Usando XML em um DataSet](using-xml-in-a-dataset.md)
- [Gravando o conteúdo do DataSet como dados XML](writing-dataset-contents-as-xml-data.md)
- [DataSets tipados](typed-datasets.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
