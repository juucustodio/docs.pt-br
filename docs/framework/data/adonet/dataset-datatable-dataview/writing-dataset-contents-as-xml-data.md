---
description: 'Saiba mais sobre: gravando conteúdo do conjunto de dados como XML'
title: Gravando o conteúdo do DataSet como dados XML
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fd15f8a5-3b4c-46d0-a561-4559ab2a4705
ms.openlocfilehash: 0ad232f744f69f822d09c0af6c4374b6e5f0147d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651360"
---
# <a name="writing-dataset-contents-as-xml-data"></a>Gravando o conteúdo do DataSet como dados XML

No ADO.NET, você pode gravar a representação XML de um <xref:System.Data.DataSet>, com ou sem seu esquema. Se as informações de esquema forem embutidas no XML embutido, elas serão gravadas através da linguagem de definição de esquema XML (XSD). O esquema contém as definições de tabela do <xref:System.Data.DataSet>, bem como as definições de relação e de restrição.  
  
 Quando um <xref:System.Data.DataSet> é gravado como dados XML, as linhas do <xref:System.Data.DataSet> são gravadas nas suas versões atuais. No entanto, o <xref:System.Data.DataSet> também pode ser gravado como um DiffGram de modo que os valores atuais e originais das linhas sejam incluídos.  
  
 A representação XML do <xref:System.Data.DataSet> pode ser gravada em um arquivo, um fluxo, um **XmlWriter** ou uma cadeia de caracteres. Essas opções proporcionam excelente flexibilidade para o transporte da representação XML do <xref:System.Data.DataSet>. Para obter a representação XML do <xref:System.Data.DataSet> como uma cadeia de caracteres, use o método **GetXml** , conforme mostrado no exemplo a seguir.  
  
```vb  
Dim xmlDS As String = custDS.GetXml()  
```  
  
```csharp  
string xmlDS = custDS.GetXml();  
```  
  
 **GetXml** retorna a representação XML do <xref:System.Data.DataSet> sem informações de esquema. Para gravar as informações de esquema do <xref:System.Data.DataSet> (como esquema XML) em uma cadeia de caracteres, use **GetXmlSchema**.  
  
 Para gravar um <xref:System.Data.DataSet> em um arquivo, fluxo ou **XmlWriter**, use o método **WriteXml** . O primeiro parâmetro que você passa para **WriteXml** é o destino da saída XML. Por exemplo, passe uma cadeia de caracteres contendo um nome de arquivo, um objeto **System. IO. TextWriter** e assim por diante. Você pode passar um segundo parâmetro opcional de um **XmlWriteMode** para especificar como a saída XML deve ser gravada.  
  
 A tabela a seguir mostra as opções para **XmlWriteMode**.  
  
|Opção de XmlWriteMode|Descrição|  
|-------------------------|-----------------|  
|**IgnoreSchema**|Grava o conteúdo atual do <xref:System.Data.DataSet> como dados XML, sem um esquema XML. Este é o padrão.|  
|**WriteSchema**|Grava o conteúdo atual do <xref:System.Data.DataSet> como dados XML com a estrutura relacional como um esquema XML embutido.|  
|**DiffGram**|Grava todo o <xref:System.Data.DataSet> como um DiffGram, incluindo valores originais e atuais. Para obter mais informações, consulte [DiffGrams](diffgrams.md).|  
  
 Ao escrever uma representação XML de um <xref:System.Data.DataSet> que contenha objetos **DataRelation** , você provavelmente desejará que o XML resultante tenha as linhas filhas de cada relação aninhada em seus elementos pai relacionados. Para fazer isso, defina a propriedade **aninhada** da **relação** como **true** quando você adicionar a **DataRelation** ao <xref:System.Data.DataSet> . Para obter mais informações, consulte [aninhando DataRelations](nesting-datarelations.md).  
  
 Veja a seguir dois exemplos de como gravar a representação XML de um <xref:System.Data.DataSet> em um arquivo. O primeiro exemplo passa o nome do arquivo para o XML resultante como uma cadeia de caracteres para **WriteXml**. O segundo exemplo passa um objeto **System. IO. StreamWriter** .
  
```vb  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema)  
```  
  
```csharp  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema);  
```  
  
```vb  
Dim xmlSW As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xml")  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema)  
xmlSW.Close()  
```  
  
```csharp  
System.IO.StreamWriter xmlSW = new System.IO.StreamWriter("Customers.xml");  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema);  
xmlSW.Close();  
```  
  
## <a name="mapping-columns-to-xml-elements-attributes-and-text"></a>Mapeando colunas para elementos XML, atributos e texto  

 Você pode especificar como uma coluna de uma tabela é representada em XML usando a propriedade **ColumnMapping** do objeto **DataColumn** . A tabela a seguir mostra os valores de **MappingType** diferentes para a propriedade **ColumnMapping** de uma coluna de tabela e o XML resultante.  
  
|Valor de MappingType|Descrição|  
|-----------------------|-----------------|  
|**Element**|Este é o padrão. A coluna é gravada como um elemento XML, em que ColumnName é o nome do elemento e o conteúdo da coluna é gravado como texto do elemento. Por exemplo:<br /><br /> `<ColumnName>Column Contents</ColumnName>`|  
|**Atributo**|A coluna é gravada como um atributo XML do elemento XML da linha atual, em que ColumnName é o nome do atributo e o conteúdo da coluna é gravado como valor do atributo. Por exemplo:<br /><br /> `<RowElement ColumnName="Column Contents" />`|  
|**SimpleContent**|O conteúdo de coluna é gravado como texto no elemento XML da linha atual. Por exemplo:<br /><br /> `<RowElement>Column Contents</RowElement>`<br /><br /> Observe que **simpleContent** não pode ser definido para uma coluna de uma tabela que tenha colunas de **elementos** ou relações aninhadas.|  
|**Oculto**|A coluna não é gravada na saída XML.|  
  
## <a name="see-also"></a>Consulte também

- [Usando XML em um DataSet](using-xml-in-a-dataset.md)
- [DiffGrams](diffgrams.md)
- [Aninhamento de DataRelations](nesting-datarelations.md)
- [Gravar informações de esquema de DataSet como XSD](writing-dataset-schema-information-as-xsd.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
