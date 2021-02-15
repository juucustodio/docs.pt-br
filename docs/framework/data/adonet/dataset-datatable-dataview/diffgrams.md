---
description: 'Saiba mais sobre: DiffGrams'
title: DiffGrams
ms.date: 03/30/2017
ms.assetid: 037f3991-7bbc-424b-b52e-8b03585d3e34
ms.openlocfilehash: df00bbfb2c25014ff4e73a2777511bd3593ff8a4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652504"
---
# <a name="diffgrams"></a>DiffGrams

Um DiffGram é um formato XML que identifica as versões atuais e originais dos elementos de dados. O <xref:System.Data.DataSet> usa o formato DiffGram para carregar e manter seu conteúdo e para serializar seu conteúdo para transporte em uma conexão de rede. Quando um <xref:System.Data.DataSet> é escrito como um DiffGram, ele popula o DiffGram com todas as informações necessárias para recriar com precisão o conteúdo, embora não o esquema, do <xref:System.Data.DataSet> , incluindo valores de coluna das versões de linha **original** e **atual** , informações de erro de linha e ordem de linha.  
  
 Ao enviar e recuperar um <xref:System.Data.DataSet> de um serviço Web XML, o formato DiffGram é usado implicitamente. Além disso, ao carregar o conteúdo de um <xref:System.Data.DataSet> XML usando o método **ReadXml** ou ao gravar o conteúdo de um <xref:System.Data.DataSet> em XML usando o método **WriteXml** , você pode especificar que o conteúdo seja lido ou gravado como um DiffGram. Para obter mais informações, consulte [carregando um conjunto de dados a partir de XML](loading-a-dataset-from-xml.md) e [gravando conteúdo do DataSet como XML](writing-dataset-contents-as-xml-data.md).  
  
 Embora o formato DiffGram seja usado principalmente pelo .NET Framework como um formato de serialização para o conteúdo de um <xref:System.Data.DataSet> , você também pode usar DiffGrams para modificar dados em tabelas em um banco de dados Microsoft SQL Server.  
  
 Um DiffGram é gerado pela gravação do conteúdo de todas as tabelas em um **\<diffgram>** elemento.  
  
### <a name="to-generate-a-diffgram"></a>Para gerar um DiffGram  
  
1. Gerar uma lista de tabelas raiz (ou seja, tabelas sem qualquer pai).  
  
2. Para cada tabela e seus descendentes na lista, anote a versão atual de todas as linhas na primeira seção DiffGram.  
  
3. Para cada tabela no <xref:System.Data.DataSet> , anote a versão original de todas as linhas, se houver, na **\<before>** seção do DiffGram.  
  
4. Para linhas com erros, grave o conteúdo de erro na **\<errors>** seção do DiffGram.  
  
 Um DiffGram é processado na ordem do início do arquivo XML até o fim.  
  
### <a name="to-process-a-diffgram"></a>Para processar um DiffGram  
  
1. Processar a primeira seção do DiffGram que contém a versão atual das linhas.  
  
2. Processe a segunda ou a **\<before>** seção que contém a versão de linha original das linhas modificadas e excluídas.  
  
    > [!NOTE]
    > Se uma linha for marcada como excluída, a operação de exclusão também poderá excluir os descendentes da linha, dependendo da `Cascade` Propriedade do atual <xref:System.Data.DataSet> .  
  
3. Processe a **\<errors>** seção. Defina as informações de erro para a linha e a coluna especificadas para cada item nesta seção.  
  
> [!NOTE]
> Se você definir <xref:System.Data.XmlWriteMode> como DiffGram, o conteúdo do destino <xref:System.Data.DataSet> e o original <xref:System.Data.DataSet> poderão ser diferentes.  
  
## <a name="diffgram-format"></a>Formato DiffGram  

 O formato DiffGram é dividido em três seções: os dados atuais, os dados originais (ou "anteriores") e uma seção de erros, conforme mostrado no exemplo a seguir.  
  
```xml  
<?xml version="1.0"?>  
<diffgr:diffgram
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  
   <DataInstance>  
   </DataInstance>  
  
  <diffgr:before>  
  </diffgr:before>  
  
  <diffgr:errors>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
 O formato DiffGram consiste nos seguintes blocos de dados:  
  
 **\<**  **_DataInstance_*_  _*>**  
 O nome desse elemento, ***DataInstance** _, é usado para fins explicativos nesta documentação. Um elemento _*_DataInstance_*_ representa uma <xref:System.Data.DataSet> ou uma linha de um <xref:System.Data.DataTable> . Em vez de _DataInstance *, o elemento conterá o nome do <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> . Esse bloco do formato DiffGram contém os dados atuais, se eles foram modificados ou não. Um elemento, ou linha, que foi modificado, é identificado com a anotação **diffgr: hasChanges** .  
  
 **\<diffgr:before>**  
 Esse bloco do formato DiffGram contém a versão original de uma linha. Os elementos neste bloco são correspondidos aos elementos no bloco ***DataInstance** _ usando a anotação _ *diffgr: ID**.  
  
 **\<diffgr:errors>**  
 Esse bloco do formato DiffGram contém informações de erro para uma linha específica no bloco ***DataInstance** _. Os elementos neste bloco são correspondidos aos elementos no bloco _*_DataInstance_*_ usando a anotação _ *diffgr: ID**.  
  
## <a name="diffgram-annotations"></a>Anotações de DiffGram  

 Os DiffGrams usam várias anotações para relacionar os elementos dos diferentes blocos de DiffGram que representam diferentes versões de linha ou informações de erro no <xref:System.Data.DataSet> .  
  
 A tabela a seguir descreve as anotações de DiffGram que são definidas no namespace do DiffGram **urn: schemas-microsoft-com: XML-DiffGram-v1**.  
  
|Annotation|Descrição|  
|----------------|-----------------|  
|**id**|Usado para emparelhar os elementos nos **\<diffgr:before>** **\<diffgr:errors>** blocos e para os elementos no **\<** **_DataInstance_*_ _*>** bloco. Os valores com a anotação **diffgr: ID** estão no formato *[TableName] [ID do @ identificador]*. Por exemplo, `<Customers diffgr:id="Customers1">`.|  
|**parentId**|Identifica qual elemento do **\<** **_DataInstance_*_ _*>** bloco é o elemento pai do elemento atual. Os valores com a anotação **diffgr: parentID** estão no formato *[TableName] [ID do @ identificador]*. Por exemplo, `<Orders diffgr:parentId="Customers1">`.|  
|**hasChanges**|Identifica uma linha no **\<** **_DataInstance_*_ _*>** bloco como modificada. A anotação **HasChanges** pode ter um dos dois valores a seguir:<br /><br /> **inserido**<br /> Identifica uma linha **adicionada** .<br /><br /> **modificado**<br /> Identifica uma linha **modificada** que contém uma versão de linha **original** no **\<diffgr:before>** bloco. Observe que as linhas **excluídas** terão uma versão de linha **original** no **\<diffgr:before>** bloco, mas não haverá nenhum elemento anotado no **\<** **_DataInstance_*_ _*>** bloco.|  
|**hasErrors**|Identifica uma linha no **\<** **_DataInstance_*_ _*>** bloco com um rowgroup . O elemento error é colocado no **\<diffgr:errors>** bloco.|  
|**Erro**|Contém o texto do **Usererror** para um elemento específico no **\<diffgr:errors>** bloco.|  
  
 O <xref:System.Data.DataSet> inclui anotações adicionais ao ler ou gravar seu conteúdo como um DiffGram. A tabela a seguir descreve essas anotações adicionais, que são definidas no namespace **urn: schemas-microsoft-com: xml-msdata**.  
  
|Annotation|Descrição|  
|----------------|-----------------|  
|**RowOrder**|Preserva a ordem de linha dos dados originais e identifica o índice de uma linha em um determinado <xref:System.Data.DataTable> .|  
|**Oculto**|Identifica uma coluna como tendo uma propriedade **ColumnMapping** definida como **MappingType. Hidden**. O atributo é escrito no formato **MSDATA: Hidden** *[ColumnName]*= "*Value*". Por exemplo, `<Customers diffgr:id="Customers1" msdata:hiddenContactTitle="Owner">`.<br /><br /> Observe que as colunas ocultas só serão gravadas como um atributo DiffGram se eles contiverem dados. Caso contrário, eles serão ignorados.|  
  
## <a name="sample-diffgram"></a>DiffGram de exemplo  

 Um exemplo do formato DiffGram é mostrado abaixo. Este exemplo mostra o resultado de uma atualização para uma linha em uma tabela antes que as alterações sejam confirmadas. A linha com um CustomerID de "ALFKI" foi modificada, mas não foi atualizada. Como resultado, há uma linha **atual** com um **diffgr: ID** de "Customers1" no **\<** **_DataInstance_*_ _*>** bloco e uma linha **original** com um **diffgr: ID** de "Customers1" no **\<diffgr:before>** bloco. A linha com um CustomerID de "ANATR" inclui um **rowgroup, portanto**, ele é anotado com `diffgr:hasErrors="true"` e há um elemento relacionado no **\<diffgr:errors>** bloco.  
  
```xml  
<diffgr:diffgram xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
  <CustomerDataSet>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0" diffgr:hasChanges="modified">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>New Company</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers2" msdata:rowOrder="1" diffgram:hasErrors="true">  
      <CustomerID>ANATR</CustomerID>  
      <CompanyName>Ana Trujillo Emparedados y Helados</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers3" msdata:rowOrder="2">  
      <CustomerID>ANTON</CustomerID>  
      <CompanyName>Antonio Moreno Taquera</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers4" msdata:rowOrder="3">  
      <CustomerID>AROUT</CustomerID>  
      <CompanyName>Around the Horn</CompanyName>  
    </Customers>  
  </CustomerDataSet>  
  <diffgr:before>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>Alfreds Futterkiste</CompanyName>  
    </Customers>  
  </diffgr:before>  
  <diffgr:errors>  
    <Customers diffgr:id="Customers2" diffgr:Error="An optimistic concurrency violation has occurred for this row."/>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
## <a name="see-also"></a>Consulte também

- [Usando XML em um DataSet](using-xml-in-a-dataset.md)
- [Carregando um DataSet a partir de XML](loading-a-dataset-from-xml.md)
- [Gravando o conteúdo do DataSet como dados XML](writing-dataset-contents-as-xml-data.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
