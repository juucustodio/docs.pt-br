---
description: 'Saiba mais sobre: adicionando DataRelations'
title: Adicionando DataRelations
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a4a564fb-c1c4-4135-b6c2-b030e51195e4
ms.openlocfilehash: 56438c9b69fab71c4843582b6cfea50fa057eb44
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99725214"
---
# <a name="adding-datarelations"></a>Adicionando DataRelations

Em um <xref:System.Data.DataSet> com vários objetos <xref:System.Data.DataTable>, você pode usar objetos <xref:System.Data.DataRelation> para relacionar uma tabela a outra, para navegar pelas tabelas e para retornar as linhas filho ou pai de uma tabela relacionada.  
  
 Os argumentos necessários para criar uma **DataRelation** são um nome para a **DataRelation** que está sendo criada e uma matriz de uma ou mais <xref:System.Data.DataColumn> referências às colunas que servem como as colunas pai e filho na relação. Depois de criar uma **DataRelation**, você pode usá-la para navegar entre tabelas e recuperar valores.  
  
 Adicionar uma **DataRelation** a um <xref:System.Data.DataSet> ADDS, por padrão, a <xref:System.Data.UniqueConstraint> à tabela pai e a <xref:System.Data.ForeignKeyConstraint> à tabela filho. Para obter mais informações sobre essas restrições padrão, consulte as [restrições de DataTable](datatable-constraints.md).  
  
 O exemplo de código a seguir cria uma **DataRelation** usando dois <xref:System.Data.DataTable> objetos em um <xref:System.Data.DataSet> . Cada <xref:System.Data.DataTable> contém uma coluna chamada **CustID**, que serve como um link entre os dois <xref:System.Data.DataTable> objetos. O exemplo adiciona uma única **DataRelation** à coleção **Relations** do <xref:System.Data.DataSet> . O primeiro argumento no exemplo especifica o nome da **DataRelation** que está sendo criada. O segundo argumento define a **DataColumn** pai e o terceiro argumento define o filho **DataColumn**.  
  
```vb  
customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustID"), _  
  customerOrders.Tables("Orders").Columns("CustID"))  
```  
  
```csharp  
customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustID"],  
  customerOrders.Tables["Orders"].Columns["CustID"]);  
```  
  
 Uma **DataRelation** também tem uma propriedade **aninhada** que, quando definida como **true**, faz com que as linhas da tabela filho sejam aninhadas dentro da linha associada da tabela pai quando gravadas como elementos XML usando <xref:System.Data.DataSet.WriteXml%2A> . Para obter mais informações, consulte [Using XML in a DataSet](using-xml-in-a-dataset.md) (Usando XML em um DataSet).  
  
## <a name="see-also"></a>Consulte também

- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
