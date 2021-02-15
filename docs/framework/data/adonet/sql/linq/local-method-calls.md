---
description: 'Saiba mais sobre: chamadas de método local'
title: Chamadas de método locais
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c34b5012-aee9-4994-9364-1d99d12b7463
ms.openlocfilehash: 7f3870a700ac86e87e3464f0bc6aaccbb2525168
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695535"
---
# <a name="local-method-calls"></a>Chamadas de método locais

Um chamada de método local é uma chamada que é executada dentro do modelo do objeto. Um chamada de método remoto é uma chamada que o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] converte no SQL e passa para o mecanismo de banco de dados para execução. As chamadas de método local são necessárias quando [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o não pode converter a chamada em SQL. Caso contrário, um <xref:System.InvalidOperationException> será gerado.  
  
## <a name="example-1"></a>Exemplo 1  

 No exemplo a seguir, uma classe `Order` é mapeada para a tabela Orders no banco de dados de exemplo Northwind. Um método de instância local foi adicionado à classe.  
  
 Em Query 1, o construtor da classe `Order` é executado localmente. Na consulta 2, se você [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tentou traduzir `LocalInstanceMethod()` no SQL, a tentativa falharia e uma <xref:System.InvalidOperationException> exceção seria gerada. Mas como o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fornece suporte para chamadas de método local, o Query2 não lançará uma exceção.  
  
 [!code-csharp[DlinqLocalMethodCall#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqLocalMethodCall/cs/Program.cs#1)]
 [!code-vb[DlinqLocalMethodCall#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqLocalMethodCall/vb/Module1.vb#1)]  
  
 [!code-csharp[DlinqLocalMethodCall#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqLocalMethodCall/cs/northwind.cs#2)]
 [!code-vb[DlinqLocalMethodCall#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqLocalMethodCall/vb/northwind.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
