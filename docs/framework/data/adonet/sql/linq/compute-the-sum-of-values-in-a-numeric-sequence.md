---
description: 'Saiba mais sobre: calcular a soma dos valores em uma sequência numérica'
title: Calcular a soma dos valores em uma sequência numérica
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 24e335b0-984e-4825-8721-0a91b533b7c3
ms.openlocfilehash: c4eb066b9286335111d96d32437291da9ea2d49a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712539"
---
# <a name="compute-the-sum-of-values-in-a-numeric-sequence"></a>Calcular a soma dos valores em uma sequência numérica

Use o operador <xref:System.Linq.Enumerable.Sum%2A> para calcular a soma de valores numéricos em uma sequência.  
  
 Observe as seguintes características do operador `Sum` no [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]:  
  
- O operador de agregação do operador de consulta padrão `Sum` avalia uma sequência vazia ou uma sequência que contém somente nulos como zero. No [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], a semântica do SQL é deixada inalterada. Por esse motivo, `Sum` avalia como nulo em vez de zero para uma sequência vazia ou para uma sequência que contém somente nulos.  
  
- As limitações do SQL em resultados intermediários se aplicam às agregações no [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. A soma das quantidades de inteiros de 32 bits não é calculada usando resultados de 64 bits, e pode ocorrer estouro para a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tradução de `Sum` . Essa possibilidade existe mesmo se a implementação do operador de consulta padrão não causa um estouro para a sequência correspondente na memória.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir localiza o frete total de todos os pedidos na tabela `Order`.  
  
 Se você executar essa consulta no banco de dados de exemplo do Northwind, a saída será: `64942.6900`.  
  
 [!code-csharp[DLinqQueryExamples#12](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#12)]
 [!code-vb[DLinqQueryExamples#12](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#12)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir localiza o número total de unidades no pedido para todos os produtos.  
  
 Se você executar essa consulta no banco de dados de exemplo do Northwind, a saída será: `780`.  
  
 Observe que você deve converter tipos `short` (por exemplo, `UnitsOnOrder`) porque `Sum` não tem sobrecarga para tipos curtos.  
  
 [!code-csharp[DLinqQueryExamples#13](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#13)]
 [!code-vb[DLinqQueryExamples#13](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#13)]  
  
## <a name="see-also"></a>Consulte também

- [Consultas de agregação](aggregate-queries.md)
- [Baixar bancos de dados de amostra](downloading-sample-databases.md)
