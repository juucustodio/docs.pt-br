---
description: 'Saiba mais sobre: como chamar funções de User-Defined embutidas'
title: 'Como: chamar funções embutidas definidas pelo usuário'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f80d4327-b6a5-4aa8-a743-e95d09a2a02e
ms.openlocfilehash: 2a7cf185af05a1ed58a2dd3b365a5bbcaa2a4fd5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786050"
---
# <a name="how-to-call-user-defined-functions-inline"></a>Como: chamar funções embutidas definidas pelo usuário

Embora você possa chamar funções definidas pelo usuário embutidos, as funções que são incluídas em uma consulta cuja execução é adiada não são executadas até que a consulta. Para obter mais informações, consulte [Introdução a Consultas de LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
 Quando você chama a mesma função fora de uma consulta, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] cria uma consulta simples de expressão de chamada de método. A seguir está a sintaxe do SQL (parâmetro `@p0` é associado à constante passada dentro):  
  
```sql  
SELECT dbo.ReverseCustName(@p0)  
```  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] cria o seguinte:  
  
 [!code-csharp[DLinqUDFS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/Program.cs#4)]
 [!code-vb[DLinqUDFS#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/Module1.vb#4)]  
  
## <a name="example"></a>Exemplo  

 Na consulta a seguir [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] , você pode ver uma chamada embutida para o método de função definido pelo usuário gerado `ReverseCustName` . A função não é executada imediatamente porque a execução da consulta é adiada. O SQL compilado para esta consulta converte a uma chamada para a função definida pelo usuário na base de dados (consulte o código SQL seguir a consulta).  
  
 [!code-csharp[DLinqUDFS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/Program.cs#5)]
 [!code-vb[DLinqUDFS#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/Module1.vb#5)]  
  
```sql  
SELECT [t0].[ContactName],  
    dbo.ReverseCustName([t0].[ContactTitle]) AS [Title]  
FROM [Customers] AS [t0]  
```  
  
## <a name="see-also"></a>Consulte também

- [Funções definidas pelo usuário](user-defined-functions.md)
