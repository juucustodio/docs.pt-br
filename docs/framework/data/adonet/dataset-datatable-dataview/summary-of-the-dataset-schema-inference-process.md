---
description: 'Saiba mais sobre: Resumo do processo de inferência de esquema do conjunto de informações'
title: Resumo do processo de inferência de esquema de DataSet
ms.date: 03/30/2017
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
ms.openlocfilehash: 637e4325558708c15d6d4eb17de9c0cf13b3b256
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651555"
---
# <a name="summary-of-the-dataset-schema-inference-process"></a>Resumo do processo de inferência de esquema de DataSet

O processo de inferência determina primeiro, a partir do documento XML, quais elementos serão inferidos como tabelas. Do XML restante, o processo de inferência determina as colunas para essas tabelas. Para tabelas aninhadas, o processo de inferência gera objetos aninhados <xref:System.Data.DataRelation> e <xref:System.Data.ForeignKeyConstraint> .  
  
 Veja a seguir um breve resumo das regras de inferência:  
  
- Elementos que têm atributos são inferidos como tabelas.  
  
- Elementos que têm elementos filho são inferidos como tabelas.  
  
- Elementos que se repetem são inferidos como uma única tabela.  
  
- Se o documento, ou raiz, o elemento não tiver atributos e nenhum elemento filho que fosse inferido como colunas, ele será inferido como um <xref:System.Data.DataSet> . Caso contrário, o elemento Document é inferido como uma tabela.  
  
- Os atributos são inferidos como colunas.  
  
- Elementos que não têm atributos ou elementos filho, e que não se repetem, são inferidos como colunas.  
  
- Para elementos que são inferidos como tabelas aninhadas dentro de outros elementos que também são inferidos como tabelas, uma **DataRelation** aninhada é criada entre as duas tabelas. Uma nova coluna de chave primária chamada **TableName_Id** é adicionada às duas tabelas e usada pela **DataRelation**. Um **ForeignKeyConstraint** é criado entre as duas tabelas usando a coluna **TableName_Id** .  
  
- Para elementos que são inferidos como tabelas e que contêm texto, mas não têm elementos filho, uma nova coluna chamada **TableName_Text** é criada para o texto de cada um dos elementos. Se um elemento for inferido como uma tabela e tiver texto, mas também tiver elementos filho, o texto será ignorado.  
  
## <a name="see-also"></a>Consulte também

- [Inferir a estrutura relacional do DataSet do esquema XML](inferring-dataset-relational-structure-from-xml.md)
- [Carregando um DataSet a partir de XML](loading-a-dataset-from-xml.md)
- [Carregando informações do esquema de DataSet do XML](loading-dataset-schema-information-from-xml.md)
- [Usando XML em um DataSet](using-xml-in-a-dataset.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
