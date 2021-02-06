---
description: 'Saiba mais sobre: carregando informações de esquema de conjunto de dados do XML'
title: Carregando informações do esquema de DataSet do XML
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 43dfb23b-5cef-46f2-8d87-78f0fba1eb8c
ms.openlocfilehash: dd3a327270d6f8e3086d7206dd6f44290415c55e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652101"
---
# <a name="loading-dataset-schema-information-from-xml"></a>Carregando informações do esquema de DataSet do XML

O esquema de <xref:System.Data.DataSet> (suas tabelas, colunas, relações e restrições) pode ser definido programaticamente, criado pelos métodos **Fill** ou **FillSchema** de um <xref:System.Data.Common.DataAdapter> , ou carregado de um documento XML. Para carregar as informações de esquema de **conjunto** de dados de um documento XML, você pode usar o método **ReadXmlSchema** ou **InferXmlSchema** do **conjunto**. O **ReadXmlSchema** permite carregar ou inferir informações de esquema de **conjunto** de dados do documento que contém o esquema XSD (linguagem de definição de esquema XML) ou um documento XML com esquema XML embutido. O **InferXmlSchema** permite inferir o esquema do documento XML enquanto ignora determinados namespaces XML que você especificar.  
  
> [!NOTE]
> A ordenação de tabela em um conjunto de um **DataSet** pode não ser preservada quando você usa Web Services ou serialização XML para transferir um conjunto de um **DataSet** que foi criado na memória usando construções XSD (como relações aninhadas). Portanto, o destinatário do **conjunto** de um não deve depender da ordenação de tabela nesse caso. No entanto, a ordenação de tabela sempre será preservada se o esquema do conjunto de um **DataSet** que está sendo transferido tiver sido lido de arquivos XSD, em vez de ser criado na memória.  
  
## <a name="readxmlschema"></a>ReadXmlSchema  

 Para carregar o esquema de um **conjunto** de dados de um documento XML sem carregar nenhum dado, você pode usar o método **ReadXmlSchema** do **DataSet**. O **ReadXmlSchema** cria o esquema de **conjunto de conjuntos** definido usando o esquema XSD (XML Schema Definition Language).  
  
 O método **ReadXmlSchema** usa um único argumento de um nome de arquivo, um fluxo ou um **XmlReader** que contém o documento XML a ser carregado. O documento XML pode conter somente o esquema ou pode conter o esquema embutido com elementos XML que contêm dados. Para obter detalhes sobre como gravar o esquema embutido como esquema XML, consulte [derivando a estrutura relacional do conjunto de dados do esquema XML (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md).  
  
 Se o documento XML passado para **ReadXmlSchema** não contiver informações de esquema embutidas, **ReadXmlSchema** inferirá o esquema dos elementos no documento XML. Se o **conjunto** de usuários já contiver um esquema, o esquema atual será estendido adicionando novas tabelas se elas ainda não existirem. As novas colunas não serão adicionadas às tabelas existentes. Se uma coluna que está sendo adicionada já existir no **conjunto** de um, mas tiver um tipo incompatível com a coluna encontrada no XML, uma exceção será lançada. Para obter detalhes sobre como o **ReadXmlSchema** infere um esquema de um documento XML, consulte [inferindo a estrutura relacional do conjunto de dados do XML](inferring-dataset-relational-structure-from-xml.md).  
  
 Embora **ReadXmlSchema** carregue ou infere apenas o esquema de um **conjunto** de dados, o método **ReadXml** do **conjunto** de dados carrega ou infere tanto o esquema quanto o dado contido no documento XML. Para obter mais informações, consulte [carregando um conjunto de dados de XML](loading-a-dataset-from-xml.md).  
  
 Os exemplos de código a seguir mostram como carregar um esquema de **conjunto** de uma de um documento ou fluxo XML. O primeiro exemplo mostra um nome de arquivo de esquema XML que está sendo passado para o método **ReadXmlSchema** . O segundo exemplo mostra um **System. IO. StreamReader**.  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXmlSchema("schema.xsd")  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.ReadXmlSchema("schema.xsd");  
```  
  
```vb  
Dim xmlStream As New System.IO.StreamReader("schema.xsd")
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXmlSchema(xmlStream)  
xmlStream.Close()  
```  
  
```csharp  
System.IO.StreamReader xmlStream = new System.IO.StreamReader("schema.xsd");  
DataSet dataSet = new DataSet();  
dataSet.ReadXmlSchema(xmlStream);  
xmlStream.Close();  
```  
  
## <a name="inferxmlschema"></a>InferXmlSchema  

 Você também pode instruir o **conjunto** de um para inferir seu esquema de um documento XML usando o método **InferXmlSchema** do **conjunto** de um. **InferXmlSchema** funcionará da mesma forma que o **ReadXml** com um **XmlReadMode** de **InferSchema** (carrega dados e também o esquema de inferência) e **ReadXmlSchema** se o documento que está sendo lido não contiver nenhum esquema embutido. No entanto, o **InferXmlSchema** fornece a capacidade adicional de permitir que você especifique namespaces XML específicos a serem ignorados quando o esquema for inferido. **InferXmlSchema** usa dois argumentos obrigatórios: o local do documento XML, especificado por um nome de arquivo, um fluxo ou um **XmlReader**; e uma matriz de cadeia de caracteres de namespaces XML a ser ignorada pela operação.  
  
 Por exemplo, considere o seguinte XML:  
  
```xml  
<NewDataSet xmlns:od="urn:schemas-microsoft-com:officedata">  
<Categories>  
  <CategoryID od:adotype="3">1</CategoryID>
  <CategoryName od:maxLength="15" od:adotype="130">Beverages</CategoryName>
  <Description od:adotype="203">Soft drinks and teas</Description>
</Categories>  
<Products>  
  <ProductID od:adotype="20">1</ProductID>
  <ReorderLevel od:adotype="3">10</ReorderLevel>
  <Discontinued od:adotype="11">0</Discontinued>
</Products>  
</NewDataSet>  
```  
  
 Devido aos atributos especificados para os elementos no documento XML anterior, o método **ReadXmlSchema** e o método **ReadXml** com um **XmlReadMode** de **InferSchema** criarão tabelas para cada elemento no documento: **Categories**, **CategoryID**, **CategoryName**, **Description**, **Products**, **ProductID**, **ReorderLevel** e **Discontinued**. (Para obter mais informações, consulte [inferindo a estrutura relacional do conjunto de dados de XML](inferring-dataset-relational-structure-from-xml.md).) No entanto, uma estrutura mais apropriada seria criar apenas as tabelas **Categories** e **Products** e, em seguida, criar colunas **CategoryID**, **CategoryName** e **Description** na tabela **Categories** , e as colunas **ProductID**, **ReorderLevel** e **Discontinued** na tabela **Products** . Para garantir que o esquema deduzido ignore os atributos especificados nos elementos XML, use o método **InferXmlSchema** e especifique o namespace XML para **officedata** a ser ignorado, conforme mostrado no exemplo a seguir.  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.InferXmlSchema("input_od.xml", New String() {"urn:schemas-microsoft-com:officedata"})  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.InferXmlSchema("input_od.xml", new string[] "urn:schemas-microsoft-com:officedata");  
```  
  
## <a name="see-also"></a>Consulte também

- [Usando XML em um DataSet](using-xml-in-a-dataset.md)
- [Derivando a estrutura relacional do DataSet do esquema XML (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [Inferir a estrutura relacional do DataSet do esquema XML](inferring-dataset-relational-structure-from-xml.md)
- [Carregando um DataSet a partir de XML](loading-a-dataset-from-xml.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
