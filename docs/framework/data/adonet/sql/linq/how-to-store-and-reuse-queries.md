---
description: 'Saiba mais sobre: como armazenar e reutilizar consultas'
title: 'Como: armazenar e reutilizar consultas'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a012bd79-1809-45e3-adea-0229532396cc
ms.openlocfilehash: a9c467cc9b2e39e6bd7616c6439d02c67f43d7c2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738813"
---
# <a name="how-to-store-and-reuse-queries"></a>Como: armazenar e reutilizar consultas

Quando você tiver um aplicativo que executa consultas estrutural semelhantes muitas vezes, você geralmente pode aumentar o desempenho criando a consulta uma hora e executando a várias vezes com parâmetros diferentes. Por exemplo, um aplicativo pode precisar recuperar todos os clientes que estão em uma cidade específica, onde cidade é especificada em runtime pelo usuário em um formulário. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dá suporte ao uso de *consultas compiladas* para essa finalidade.  
  
> [!NOTE]
> Esse padrão de uso representa o uso mais comum para consultas compilados. Outras abordagens são possíveis. Por exemplo, consultas compiladas podem ser armazenadas como membros estáticos em uma classe parcial que estende o código gerado pelo designer.  
  
## <a name="example"></a>Exemplo  

 Em muitos cenários talvez queira reutilizar as consultas através dos limites de segmento. Nesses casos, armazenar as consultas compilados em variáveis estáticas é muito eficiente. O exemplo de código a seguir pressupõe uma classe de `Queries` projetada para armazenar consultas compilados, e pressupõe uma classe Northwind que representa <xref:System.Data.Linq.DataContext>fortemente tipado.  
  
 [!code-csharp[DLinqQuerying#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#6)]
 [!code-vb[DLinqQuerying#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#6)]  
  
 [!code-csharp[DLinqQuerying#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#7)]
 [!code-vb[DLinqQuerying#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#7)]  
  
## <a name="example"></a>Exemplo  

 Atualmente, não é possível armazenar consultas (em variáveis estáticas) que retornam um *tipo anônimo*, porque o tipo não tem nome para fornecer como um argumento genérico. O exemplo a seguir mostra como você pode contornar do problema criando um tipo que pode representar o resultado, e o usar como um argumento genérico.  
  
 [!code-csharp[DLinqQuerying#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#8)]
 [!code-vb[DLinqQuerying#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#8)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.Linq.CompiledQuery>
- [Consulte conceitos](query-concepts.md)
- [Consultando o banco de dados](querying-the-database.md)
