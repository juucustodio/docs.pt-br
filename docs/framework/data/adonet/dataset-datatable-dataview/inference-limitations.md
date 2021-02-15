---
description: 'Saiba mais sobre: limitações de inferência'
title: Limitações de inferência
ms.date: 03/30/2017
ms.assetid: 78517994-5d57-44f8-9d20-38812977de09
ms.openlocfilehash: 926e456acfc5eac2598be40490b72523facfd058
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652257"
---
# <a name="inference-limitations"></a>Limitações de inferência

O processo de inferir um <xref:System.Data.DataSet> esquema do XML pode resultar em esquemas diferentes dependendo dos elementos XML em cada documento. Por exemplo, considere os documentos XML a seguir.  
  
 Documento1  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 Document2:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
</DocumentElement>  
```  
  
 Para "Documento1", o processo de inferência produz um conjunto de um **DataSet** chamado "documentElement" e uma tabela chamada "Element1", porque "Element1" é um elemento repetitivo.  
  
 **Conjunto** de um: DocumentElement  
  
 **Tabela:** Element1  
  
|Element1_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
 No entanto, para "document2", o processo de inferência produz um **conjunto de conjuntos** chamado "NewDataSet" e uma tabela denominada "documentElement". "Element1" é inferido como uma coluna porque não tem atributos nem elementos filho.  
  
 **Conjunto** de um: NewDataSet  
  
 **Tabela:** DocumentElement  
  
|Element1|  
|--------------|  
|Text1|  
  
 Esses dois documentos XML podem ter sido destinados a produzir o mesmo esquema, mas o processo de inferência produz resultados muito diferentes com base nos elementos contidos em cada documento.  
  
 Para evitar as discrepâncias que podem ocorrer ao gerar o esquema a partir de um documento XML, recomendamos que você especifique explicitamente um esquema usando XSD (linguagem de definição de esquema XML) ou XDR (XML-Data reduzido) ao carregar um conjunto de um **DataSet** de XML. Para obter mais informações sobre como especificar explicitamente um esquema de **conjunto** de dados com esquema XML, consulte [derivando a estrutura relacional do conjunto de dados do esquema XML (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md).  
  
## <a name="see-also"></a>Consulte também

- [Inferir a estrutura relacional do DataSet do esquema XML](inferring-dataset-relational-structure-from-xml.md)
- [Carregando um DataSet a partir de XML](loading-a-dataset-from-xml.md)
- [Carregando informações do esquema de DataSet do XML](loading-dataset-schema-information-from-xml.md)
- [Usando XML em um DataSet](using-xml-in-a-dataset.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
