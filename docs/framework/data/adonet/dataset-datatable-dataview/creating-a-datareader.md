---
description: 'Saiba mais sobre: Criando um DataReader'
title: Criar um DataReader
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49d4422a-7464-4ab8-8ec7-90185fde3ecf
ms.openlocfilehash: 3a9f47ce90beaa3da4c2835f8b75e770a6179a9e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99725097"
---
# <a name="creating-a-datareader"></a>Criar um DataReader

As <xref:System.Data.DataTable> <xref:System.Data.DataSet> classes e têm um <xref:System.Data.DataTable.CreateDataReader%2A> método que retorna o conteúdo do <xref:System.Data.DataTable> ou o conteúdo da <xref:System.Data.DataSet> coleção do objeto <xref:System.Data.DataSet.Tables%2A> como um ou mais conjuntos de resultados somente de encaminhamento e somente leitura.  
  
## <a name="example"></a>Exemplo  

 O aplicativo de console a seguir cria uma <xref:System.Data.DataTable> instância do. Em seguida, o exemplo passa o preenchido <xref:System.Data.DataTable> para um procedimento que chama o <xref:System.Data.DataTable.CreateDataReader%2A> método, que itera pelos resultados contidos no <xref:System.Data.DataTableReader> .  
  
 [!code-csharp[DataWorks DataTable.CreateDataReader#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTable.CreateDataReader/CS/source.cs#1)]
 [!code-vb[DataWorks DataTable.CreateDataReader#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTable.CreateDataReader/VB/source.vb#1)]  
  
 O exemplo exibe a seguinte saída na janela do console:  
  
```output  
1 Mary  
2 Andy  
3 Peter  
4 Russ  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataTable.CreateDataReader%2A>
- <xref:System.Data.DataSet.CreateDataReader%2A>
- [DataTableReaders](datatablereaders.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
