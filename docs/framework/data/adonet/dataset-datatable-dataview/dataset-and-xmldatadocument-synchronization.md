---
description: 'Saiba mais sobre: sincronização de conjunto de informações e XmlDataDocument'
title: Sincronização de DataSet e XmlDataDocument
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0ce3793d-54b2-47e4-8cf7-b0591cc4dd21
ms.openlocfilehash: c3bb1af305dfc319cb2c4783f4e4edc108e9d737
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739554"
---
# <a name="dataset-and-xmldatadocument-synchronization"></a>Sincronização de DataSet e XmlDataDocument

O ADO.NET <xref:System.Data.DataSet> fornece uma representação de dados relacional. Para obter acesso a dados hierárquicos, você pode usar as classes XML disponíveis no .NET Framework. Historicamente, essas duas representações de dados foram usadas separadamente. No entanto, o .NET Framework permite o acesso síncrono em tempo real a representações hierárquicas e relacionais de dados por meio do objeto **DataSet** e do <xref:System.Xml.XmlDataDocument> objeto, respectivamente.  
  
 Quando um **conjunto** de dados é sincronizado com um **XmlDataDocument**, ambos os objetos estão trabalhando com um único conjunto. Isso significa que, se uma alteração for feita no **conjunto** de um, a alteração será refletida no **XmlDataDocument**, e vice-versa. A relação entre o **conjunto** de aplicativos e o **XmlDataDocument** cria uma grande flexibilidade ao permitir um único aplicativo, usando um único conjunto de dados, para acessar todo o conjunto de serviços compilados em todo o **DataSet** (como Web Forms e Windows Forms controles e designers do Visual Studio .net), bem como o conjunto de serviços XML, incluindo XSL (Extensible Stylesheet Language), XSLT (transformação XSL) e XPath (XML Path Language). Você não tem que escolher qual conjunto de serviços direcionar com o aplicativo; ambos estão disponíveis.  
  
 Há várias maneiras de sincronizar um **conjunto** de uma com um **XmlDataDocument**. Você pode:  
  
- Popule um **conjunto** de dados com esquema (ou seja, uma estrutura relacional) e sincronize-os com um novo **XmlDataDocument**. Isso fornece uma exibição hierárquica de dados relacionais existentes. Por exemplo:  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema and data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema and data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    ```  
  
- Popular um **conjunto** de um DataSet somente com esquema (como um **conjunto** de um DataSet com rigidez de tipos), sincronizá-lo com um **XmlDataDocument** e, em seguida, carregar o **XmlDataDocument** de um documento XML. Isso fornece uma exibição relacional de dados hierárquicos existentes. Os nomes de tabela e de coluna no seu esquema de conjunto de seus **conjuntos** de itens devem corresponder aos nomes dos elementos XML com os quais você deseja que eles sejam sincronizados. Essa correspondência diferencia maiúsculas de minúsculas.  
  
     Observe que o esquema do **conjunto** de um só precisa corresponder aos elementos XML que você deseja expor em sua exibição relacional. Dessa maneira, você pode ter um documento XML muito grande e uma "janela" relacional muito pequena nesse documento. O **XmlDataDocument** preserva todo o documento XML, embora o **conjunto** de os apenas exponha uma pequena parte dele. (Para obter um exemplo detalhado disso, confira [sincronizando um conjunto de informações com um XmlDataDocument](synchronizing-a-dataset-with-an-xmldatadocument.md).)  
  
     O exemplo de código a seguir mostra as etapas para criar um **conjunto** de um e preencher seu esquema e, em seguida, sincronizá-lo com um **XmlDataDocument**. Observe que o esquema do **conjunto** de um só precisa corresponder aos elementos do **XmlDataDocument** que você deseja expor usando o **DataSet**.  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema, but not data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema, but not data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
     Você não poderá carregar um **XmlDataDocument** se ele estiver sincronizado com um **conjunto** de dados que contenha dado. Uma exceção será gerada.  
  
- Crie um novo **XmlDataDocument** e carregue-o de um documento XML e, em seguida, acesse a exibição relacional dos dados usando a propriedade **DataSet** de **XmlDataDocument**. Você precisa definir o esquema do **conjunto** de dados antes de poder exibir qualquer dado no **XmlDataDocument** usando o **DataSet**. Novamente, os nomes de tabela e os nomes de coluna no esquema do conjunto de seus **conjuntos** devem corresponder aos nomes dos elementos XML com os quais você deseja que eles sejam sincronizados. Essa correspondência diferencia maiúsculas de minúsculas.  
  
     O exemplo de código a seguir mostra como acessar a exibição relacional dos dados em um **XmlDataDocument**.  
  
    ```vb  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument  
    Dim dataSet As DataSet = xmlDoc.DataSet  
  
    ' Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    XmlDataDocument xmlDoc = new XmlDataDocument();  
    DataSet dataSet = xmlDoc.DataSet;  
  
    // Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
 Outra vantagem de sincronizar um **XmlDataDocument** com um **DataSet** é que a fidelidade de um documento XML é preservada. Se o **conjunto** de dados for populado a partir de um documento XML usando **ReadXml**, quando eles forem gravados como um documento XML usando o **WriteXml** , ele poderá diferir significativamente do documento XML original. Isso ocorre porque o **conjunto** de dados não mantém a formatação, como o espaço em branco, ou informações hierárquicas, como a ordem dos elementos, a partir do documento XML. O **conjunto** de os também não contém elementos do documento XML que foram ignorados porque não corresponderam ao esquema do **conjunto** de um. A sincronização de um **XmlDataDocument** com um **conjunto** de dados permite que a estrutura de elementos de formatação e hierárquica do documento XML original seja mantida no **XmlDataDocument**, enquanto o **conjunto** de dados contém apenas as informações de esquema e data apropriadas para o **DataSet**.  
  
 Ao sincronizar um **conjunto** de uma com um **XmlDataDocument**, os resultados podem diferir dependendo se seus objetos estão ou não <xref:System.Data.DataRelation> aninhados. Para obter mais informações, consulte [aninhando DataRelations](nesting-datarelations.md).  
  
## <a name="in-this-section"></a>Nesta seção  

 [Sincronizar um DataSet com um XmlDataDocument](synchronizing-a-dataset-with-an-xmldatadocument.md)  
 Demonstra a sincronização de um conjunto de um **DataSet** com rigidez de tipos, com o esquema mínimo, com um **XmlDataDocument**.  
  
 [Executar uma consulta XPath em um DataSet](performing-an-xpath-query-on-a-dataset.md)  
 Demonstra como executar uma consulta XPath no conteúdo de um **DataSet**.  
  
 [Aplicar uma transformação XSLT a um DataSet](applying-an-xslt-transform-to-a-dataset.md)  
 Demonstra a aplicação de uma transformação XSLT ao conteúdo de um **DataSet**.  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Usando XML em um DataSet](using-xml-in-a-dataset.md)  
 Descreve como o **DataSet** interage com o XML como uma fonte de dados, incluindo o carregamento e a persistência do conteúdo de um **conjunto** de dados como um dado XML.  
  
 [Aninhamento de DataRelations](nesting-datarelations.md)  
 Discute a importância de objetos **DataRelation** aninhados ao representar o conteúdo de um **DataSet** como dados XML e descreve como criar essas relações.  
  
 [DataSets, DataTables e DataViews](index.md)  
 Descreve o **DataSet** e como usá-lo para gerenciar dados de aplicativo e interagir com fontes de dados, incluindo bancos de dados relacionais e XML.  
  
 <xref:System.Xml.XmlDataDocument>  
 Contém informações de referência sobre a classe **XmlDataDocument** .  
  
## <a name="see-also"></a>Consulte também

- [Visão geral do ADO.NET](../ado-net-overview.md)
