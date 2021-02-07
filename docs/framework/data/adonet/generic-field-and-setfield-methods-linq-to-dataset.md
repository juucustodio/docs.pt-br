---
description: 'Saiba mais sobre: métodos de campo genérico e SetField (LINQ to DataSet)'
title: Campo genérico e métodos de SetField (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1883365f-9d6c-4ccb-9187-df309f47706d
ms.openlocfilehash: 2dfbb7377d782525170d47f59a5577f96caadbb6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724005"
---
# <a name="generic-field-and-setfield-methods-linq-to-dataset"></a>Campo genérico e métodos de SetField (LINQ to DataSet)

LINQ to DataSet fornece métodos de extensão à <xref:System.Data.DataRow> classe para acessar valores de coluna: o <xref:System.Data.DataRowExtensions.Field%2A> método e o <xref:System.Data.DataRowExtensions.SetField%2A> método. Esses métodos fornecem acesso mais fácil a valores de coluna para desenvolvedores, especialmente em relação a valores nulos. O <xref:System.Data.DataSet> usa <xref:System.DBNull.Value?displayProperty=nameWithType> para representar valores nulos, enquanto o LINQ usa os <xref:System.Nullable> <xref:System.Nullable%601> tipos e. Usar o acessador de coluna pré-existente no <xref:System.Data.DataRow> exige que você converta o objeto de retorno para o tipo apropriado. Se um determinado campo em um <xref:System.Data.DataRow> puder ser nulo, você deverá verificar explicitamente se há um valor nulo, pois retornando <xref:System.DBNull.Value?displayProperty=nameWithType> e convertendo-o implicitamente em outro tipo gera um <xref:System.InvalidCastException> . No exemplo a seguir, se o <xref:System.Data.DataRow.IsNull%2A?displayProperty=nameWithType> método não foi usado para verificar um valor nulo, uma exceção seria gerada se o indexador retornou <xref:System.DBNull.Value?displayProperty=nameWithType> e tentou convertê-lo em um <xref:System.String> .  
  
 [!code-csharp[DP LINQ to DataSet Examples#WhereIsNull](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#whereisnull)]
 [!code-vb[DP LINQ to DataSet Examples#WhereIsNull](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#whereisnull)]  
  
 O método <xref:System.Data.DataRowExtensions.Field%2A> fornece acesso aos valores de coluna de um <xref:System.Data.DataRow> e o <xref:System.Data.DataRowExtensions.SetField%2A> define valores de coluna em um <xref:System.Data.DataRow>. O <xref:System.Data.DataRowExtensions.Field%2A> método e o <xref:System.Data.DataRowExtensions.SetField%2A> método tratam tipos de valor anuláveis, portanto, você não precisa verificar explicitamente se há valores nulos como no exemplo anterior. Ambos os métodos também são genéricos, de modo que você não tem que converter o tipo de retorno.  
  
 O exemplo a seguir usa o método <xref:System.Data.DataRowExtensions.Field%2A>.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Where3](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#where3)]
 [!code-vb[DP LINQ to DataSet Examples#Where3](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#where3)]  
  
 Observe que o tipo de dados especificado no parâmetro genérico `T` dos métodos <xref:System.Data.DataRowExtensions.Field%2A> e <xref:System.Data.DataRowExtensions.SetField%2A> deve corresponder ao tipo do valor subjacente. Caso contrário, uma exceção <xref:System.InvalidCastException> será gerada. O nome da coluna especificado também deve corresponder ao nome de uma coluna no <xref:System.Data.DataSet> ou <xref:System.ArgumentException> será gerado. Em ambos os casos, a exceção é gerada em tempo de execução durante a enumeração dos dados quando a consulta é executada.  
  
 O próprio método <xref:System.Data.DataRowExtensions.SetField%2A> não realiza nenhuma conversão de tipos. Isso não significa, entretanto, que uma conversão de tipos não ocorrerá. O <xref:System.Data.DataRowExtensions.SetField%2A> método expõe o comportamento ADO.NET da <xref:System.Data.DataRow> classe. Uma conversão de tipo pode ser executada pelo <xref:System.Data.DataRow> objeto e o valor convertido seria então salvo no <xref:System.Data.DataRow> objeto.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Data.DataRowExtensions>
