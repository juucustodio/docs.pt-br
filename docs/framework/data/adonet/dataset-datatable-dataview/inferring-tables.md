---
description: 'Saiba mais sobre: tabelas de referência'
title: Inferir tabelas
ms.date: 03/30/2017
ms.assetid: 74a288d4-b8e9-4f1a-b2cd-10df92c1ed1f
ms.openlocfilehash: 00a24cbfc44aea4279b0a115214ec26d3eac59ad
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652153"
---
# <a name="inferring-tables"></a>Inferir tabelas

Ao inferir um esquema para um <xref:System.Data.DataSet> de um documento XML, o ADO.net primeiro determina quais elementos XML representam tabelas. As estruturas XML a seguir resultam em uma tabela para o esquema do **conjunto** de resultados:  
  
- Elementos com atributos  
  
- Elementos com elementos filho  
  
- Elementos repetitivos  
  
## <a name="elements-with-attributes"></a>Elementos com atributos  

 Elementos que têm atributos especificados neles resultam em tabelas inferidas. Por exemplo, considere o seguinte XML:  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1"/>  
  <Element1 attr1="value2">Text1</Element1>  
</DocumentElement>  
```  
  
 O processo de inferência produz uma tabela chamada "Element1".  
  
 **Conjunto** de um: DocumentElement  
  
 **Tabela:** Element1  
  
|attr1|Element1_Text|  
|-----------|--------------------|  
|value1||  
|value2|Text1|  
  
## <a name="elements-with-child-elements"></a>Elementos com elementos filho  

 Elementos que têm elementos filho resultam em tabelas inferidas. Por exemplo, considere o seguinte XML:  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
  </Element1>  
</DocumentElement>  
```  
  
 O processo de inferência produz uma tabela chamada "Element1".  
  
 **Conjunto** de um: DocumentElement  
  
 **Tabela:** Element1  
  
|ChildElement1|  
|-------------------|  
|Text1|  
  
 O elemento Document ou root resulta em uma tabela inferida se tiver atributos ou elementos filho que são inferidos como colunas. Se o elemento Document não tiver nenhum atributo e nenhum elemento filho for inferido como Columns, o elemento será inferido como um **DataSet**. Por exemplo, considere o seguinte XML:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element2>Text2</Element2>  
</DocumentElement>  
```  
  
 O processo de inferência produz uma tabela denominada "documentElement".  
  
 **Conjunto** de um: NewDataSet  
  
 **Tabela:** DocumentElement  
  
|Element1|Element2|  
|--------------|--------------|  
|Text1|Text2|  
  
 Como alternativa, considere o seguinte XML:  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 O processo de inferência produz um **conjunto de conjuntos** chamado "documentElement" que contém uma tabela chamada "Element1".  
  
 **Conjunto** de um: DocumentElement  
  
 **Tabela:** Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|value1|value2|  
  
## <a name="repeating-elements"></a>Elementos repetitivos  

 Elementos que se repetem resultam em uma única tabela inferida. Por exemplo, considere o seguinte XML:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 O processo de inferência produz uma tabela chamada "Element1".  
  
 **Conjunto** de um: DocumentElement  
  
 **Tabela:** Element1  
  
|Element1_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
## <a name="see-also"></a>Consulte também

- [Inferir a estrutura relacional do DataSet do esquema XML](inferring-dataset-relational-structure-from-xml.md)
- [Carregando um DataSet a partir de XML](loading-a-dataset-from-xml.md)
- [Carregando informações do esquema de DataSet do XML](loading-dataset-schema-information-from-xml.md)
- [Usando XML em um DataSet](using-xml-in-a-dataset.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
