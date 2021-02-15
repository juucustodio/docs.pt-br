---
description: 'Saiba mais sobre: consultando a coleção DataRowView em um DataView'
title: Consultando a coleção DataRowView em um DataView
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b9070a12-1094-44d6-bb87-a23b50bcb0af
ms.openlocfilehash: 2158e1c82c530c48d7edad71f46f03cbfe566536
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695925"
---
# <a name="querying-the-datarowview-collection-in-a-dataview"></a>Consultando a coleção DataRowView em um DataView

O <xref:System.Data.DataView> expõe uma coleção enumerável de objetos <xref:System.Data.DataRowView>. O <xref:System.Data.DataRowView> representa uma exibição personalizada do <xref:System.Data.DataRow> e exibe uma versão específica desse <xref:System.Data.DataRow> em um controle. Somente uma versão de um <xref:System.Data.DataRow> pode ser exibida em um controle, como <xref:System.Windows.Forms.DataGridView>. Você pode acessar o <xref:System.Data.DataRow> que é exposto pelo <xref:System.Data.DataRowView> por meio da propriedade <xref:System.Data.DataRowView.Row%2A> do <xref:System.Data.DataRowView>. Quando você exibe valores usando um <xref:System.Data.DataRowView>, a propriedade <xref:System.Data.DataView.RowStateFilter%2A> determina qual versão da linha do <xref:System.Data.DataRow> subjacente é exposta. Para obter informações sobre como acessar versões de linha diferentes usando um <xref:System.Data.DataRow> , consulte [Estados de linha e versões de linha](./dataset-datatable-dataview/row-states-and-row-versions.md). Como a coleção de <xref:System.Data.DataRowView> objetos expostos pelo <xref:System.Data.DataView> é enumerable, você pode usar LINQ to DataSet para consultá-lo.  
  
 O exemplo a seguir consulta produtos na cor vermelha na tabela `Product` e cria uma tabela daquela consulta. Um <xref:System.Data.DataView> é criado da tabela e a propriedade <xref:System.Data.DataView.RowStateFilter%2A> é definida para filtrar em linhas excluídas e modificadas. O <xref:System.Data.DataView> é então usado como uma origem em uma consulta LINQ, e os objetos <xref:System.Data.DataRowView> que foram modificados e excluídos são associados a um controle <xref:System.Windows.Forms.DataGridView>.  
  
 [!code-csharp[DP DataView Samples#QueryDataView2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview2)]
 [!code-vb[DP DataView Samples#QueryDataView2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview2)]  
  
 O exemplo a seguir cria uma tabela de produtos de uma exibição que está associada a um controle <xref:System.Windows.Forms.DataGridView>. Produtos na cor vermelha são consultados no <xref:System.Data.DataView> e os resultados ordenados são associados a um controle <xref:System.Windows.Forms.DataGridView>.  
  
 [!code-csharp[DP DataView Samples#QueryDataView1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview1)]
 [!code-vb[DP DataView Samples#QueryDataView1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview1)]  
  
## <a name="see-also"></a>Consulte também

- [Associação e LINQ to DataSet de dados](data-binding-and-linq-to-dataset.md)
