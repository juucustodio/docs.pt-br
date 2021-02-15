---
description: 'Saiba mais sobre: como: reutilizar uma conexão entre um comando ADO.NET e um DataContext'
title: 'Como: reutilizar uma conexão entre um comando ADO.NET e um DataContext'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7e26c7eb-c18a-43b5-a8f0-28fd8b04b0f0
ms.openlocfilehash: d5bf45dfd705ed6e9b9d4ed9659e01bfcb539df2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785946"
---
# <a name="how-to-reuse-a-connection-between-an-adonet-command-and-a-datacontext"></a>Como: reutilizar uma conexão entre um comando ADO.NET e um DataContext

Como [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o faz parte da família de tecnologias ADO.net e é baseado em serviços fornecidos pelo ADO.net, você pode reutilizar uma conexão entre um comando ADO.net e um <xref:System.Data.Linq.DataContext> .  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como reutilizar a mesma conexão entre um comando ADO.NET e o <xref:System.Data.Linq.DataContext> .  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#4)]
 [!code-vb[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#4)]  
  
## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
- [O ADO.NET e LINQ to SQL](ado-net-and-linq-to-sql.md)
- [Comunicação com o banco de dados](communicating-with-the-database.md)
