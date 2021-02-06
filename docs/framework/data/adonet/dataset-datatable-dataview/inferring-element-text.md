---
description: 'Saiba mais sobre: inferir texto de elemento'
title: Inferir o texto do elemento
ms.date: 03/30/2017
ms.assetid: 789799e5-716f-459f-a168-76c5cf22178b
ms.openlocfilehash: 5d0d9b1b3bb6164cd3cf26b429a4c7d658ee4128
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652205"
---
# <a name="inferring-element-text"></a>Inferir o texto do elemento

Se um elemento contiver texto e não tiver nenhum elemento filho a ser inferido como tabelas (como elementos com atributos ou elementos repetidos), uma nova coluna com o nome **TableName_Text** será adicionada à tabela inferida para o elemento. O texto contido no elemento será adicionado a uma linha na tabela e armazenado na nova coluna. A propriedade **ColumnMapping** da nova coluna será definida como **MappingType. simpleContent**.  
  
 Por exemplo, considere o XML a seguir.  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1">Text1</Element1>  
</DocumentElement>  
```  
  
 O processo de inferência produzirá uma tabela chamada **Element1** com duas colunas: **attr1** e **Element1_Text**. A propriedade **ColumnMapping** da coluna **attr1** será definida como **MappingType. Attribute**. A propriedade **ColumnMapping** da coluna **Element1_Text** será definida como **MappingType. simpleContent**.  
  
 **Conjunto** de um: DocumentElement  
  
 **Tabela:** Element1  
  
|attr1|Element1_Text|  
|-----------|--------------------|  
|value1|Text1|  
  
 Se um elemento contiver texto, mas também tiver elementos filho que contenham texto, uma coluna não será adicionada à tabela para armazenar o texto contido no elemento. O texto contido no elemento será ignorado, enquanto o texto nos elementos filho é incluído em uma linha na tabela. Por exemplo, considere o XML a seguir.  
  
```xml  
<Element1>  
  Text1  
  <ChildElement1>Text2</ChildElement1>  
  Text3  
</Element1>  
```  
  
 O processo de inferência produzirá uma tabela chamada **Element1** com uma coluna chamada **ChildElement1**. O texto do elemento **ChildElement1** será incluído em uma linha na tabela. O outro texto será ignorado. A propriedade **ColumnMapping** da coluna **ChildElement1** será definida como **MappingType. Element**.  
  
 **Conjunto** de um: DocumentElement  
  
 **Tabela:** Element1  
  
|ChildElement1|  
|-------------------|  
|Text2|  
  
## <a name="see-also"></a>Consulte também

- [Inferir a estrutura relacional do DataSet do esquema XML](inferring-dataset-relational-structure-from-xml.md)
- [Carregando um DataSet a partir de XML](loading-a-dataset-from-xml.md)
- [Carregando informações do esquema de DataSet do XML](loading-dataset-schema-information-from-xml.md)
- [Usando XML em um DataSet](using-xml-in-a-dataset.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
