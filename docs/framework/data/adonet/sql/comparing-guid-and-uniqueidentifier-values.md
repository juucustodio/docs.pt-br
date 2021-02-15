---
title: Comparando valores de GUID e uniqueidentifier
description: Saiba como criar e comparar valores GUID no Provedor de Dados de .NET Framework para SQL Server, que são representados pelo tipo de dados uniqueidentifier.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.openlocfilehash: 649093259747d045945c55e39edb1391708940cf
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173569"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>Comparando valores de GUID e uniqueidentifier

O tipo de dados GUID (identificador global exclusivo) no SQL Server é representado pelo tipo de dados `uniqueidentifier`, que armazena um valor binário de 16 bytes. Um GUID é um número binário cujo principal uso é como um identificador que deve ser exclusivo em uma rede com vários computadores em muitos sites. Os GUIDs podem ser gerados chamando a função NEWID do Transact-SQL e têm a garantia de serem exclusivos em todo o mundo. Para obter mais informações, confira [uniqueidentifier (Transact-SQL)](/sql/t-sql/data-types/uniqueidentifier-transact-sql).  
  
## <a name="working-with-sqlguid-values"></a>Trabalhando com valores SqlGuid  

 Já que os valores de GUIDs são longos e obscuros, eles não são significativos para os usuários. Se GUIDs gerados aleatoriamente forem usados para valores de chave e você inserir muitas linhas, você obterá E/S aleatórias em seus índices, o que poderá afetar negativamente o desempenho. Os GUIDs também são relativamente grandes quando comparados a outros tipos de dados. Em geral, recomendamos o uso de GUIDs apenas em cenários muito restritos, para os quais nenhum outro tipo de dados é adequado.  
  
### <a name="comparing-guid-values"></a>Comparando valores de GUID  

 Operadores de comparação podem ser usados com valores `uniqueidentifier`. Entretanto, a ordenação não é implementada comparando os padrões de bit dos dois valores. As únicas operações que são permitidas em relação a um `uniqueidentifier` valor são comparações (=,  <>, \<, > , \<=, > =) e verificação de NULL (é NULL e não é NULL). Nenhum outro operador aritmético é permitido.  
  
 Tanto <xref:System.Guid> quanto <xref:System.Data.SqlTypes.SqlGuid> têm um método `CompareTo` para comparar valores GUID diferentes. No entanto, `System.Guid.CompareTo` e `SqlTypes.SqlGuid.CompareTo` são implementados de maneiras diferentes. <xref:System.Data.SqlTypes.SqlGuid> implementa `CompareTo` usando o comportamento do SQL Server, no qual apenas os últimos seis bytes de um valor são mais significativos. <xref:System.Guid> avalia todos os 16 bytes. O exemplo a seguir demonstra essa diferença de comportamento. A primeira seção do código exibe valores de <xref:System.Guid> não classificados e a segunda seção do código mostra os valores de <xref:System.Guid> classificados. A terceira seção mostra os valores de <xref:System.Data.SqlTypes.SqlGuid> classificados. A saída é exibida abaixo da listagem de código.  
  
 [!code-csharp[DataWorks SqlTypes.Guid#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.Guid/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.Guid#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.Guid/VB/source.vb#1)]  
  
 Esse exemplo gera os resultados a seguir.  
  
```output  
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## <a name="see-also"></a>Confira também

- [Tipos de dados do SQL Server e ADO.NET](sql-server-data-types.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
