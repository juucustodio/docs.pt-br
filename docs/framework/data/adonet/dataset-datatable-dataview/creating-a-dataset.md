---
description: 'Saiba mais sobre: Criando um conjunto de informações'
title: Criando um DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 57629d8f-393e-4677-8b83-29ffde27f5fc
ms.openlocfilehash: 7a52c6e73b5ab3ba4bf384d6bab3640b85929fcc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739645"
---
# <a name="creating-a-dataset"></a>Criando um DataSet

Você cria uma instância de um <xref:System.Data.DataSet> chamando o construtor <xref:System.Data.DataSet>. Opcionalmente especifique um argumento de nome. Se você não especificar um nome para o <xref:System.Data.DataSet>, o nome será definido como "NewDataSet".  
  
 Você também pode criar um novo <xref:System.Data.DataSet> baseado em um <xref:System.Data.DataSet> existente. O novo <xref:System.Data.DataSet> pode ser uma cópia exata do <xref:System.Data.DataSet> existente; um clone do <xref:System.Data.DataSet> que copia a estrutura relacional ou o esquema, mas que não contém nenhum dos dados do <xref:System.Data.DataSet> existente; ou um subconjunto de <xref:System.Data.DataSet>, que contém somente as linhas modificadas do <xref:System.Data.DataSet> existente usando o método <xref:System.Data.DataSet.GetChanges%2A>. Para obter mais informações, consulte [copiando conteúdo do conjunto](copying-dataset-contents.md)de dados.  
  
 O exemplo de código a seguir demonstra como criar uma instância de um <xref:System.Data.DataSet>.  
  
```vb  
Dim customerOrders As DataSet = New DataSet("CustomerOrders")  
```  
  
```csharp  
DataSet customerOrders = new DataSet("CustomerOrders");  
```  
  
## <a name="see-also"></a>Consulte também

- [Populando um DataSet a partir de um DataAdapter](../populating-a-dataset-from-a-dataadapter.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
