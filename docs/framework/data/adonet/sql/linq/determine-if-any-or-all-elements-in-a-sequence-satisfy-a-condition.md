---
description: 'Saiba mais sobre: determinar se algum ou todos os elementos em uma sequência atendem a uma condição'
title: Determinar se alguns ou todos os elementos em uma sequência satisfazem uma condição
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 339ec145-826c-46d2-8cf2-3acd252cd072
ms.openlocfilehash: a46cf7e4e213eba830dc203f9266a408103cee80
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786102"
---
# <a name="determine-if-any-or-all-elements-in-a-sequence-satisfy-a-condition"></a>Determinar se alguns ou todos os elementos em uma sequência satisfazem uma condição

O operador de <xref:System.Linq.Enumerable.All%2A> retorna `true` se todos os elementos em uma sequência satisfazem uma condição.  
  
 O operador de <xref:System.Linq.Queryable.Any%2A> retorna `true` se qualquer elemento em uma sequência satisfazem uma condição.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir retorna uma sequência de clientes que possuem pelo menos um pedido. A `Where` / `where` cláusula é avaliada `true` como se a fornecida `Customer` tiver alguma `Order` .  
  
 [!code-csharp[DLinqQueryExamples#37](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#37)]
 [!code-vb[DLinqQueryExamples#37](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#37)]  
  
## <a name="example"></a>Exemplo  

 O seguinte código de Visual Basic determina a lista de clientes que não colocaram pedidos, e assegura que para cada cliente na lista, um nome de contato é fornecido.  
  
 [!code-vb[DLinqQueryExamples#37v](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#37v)]  
  
## <a name="example"></a>Exemplo  

 O exemplo de C# retorna uma sequência de clientes cujos pedidos têm `ShipCity` que começa com “C 2.0”. Também são incluídos no retorno clientes que não têm nenhum pedido. (Por design, o <xref:System.Linq.Queryable.All%2A> operador retorna `true` para uma sequência vazia.) Clientes sem pedidos são eliminados na saída do console usando o `Count` operador.  
  
 [!code-csharp[DLinqQueryExamples#38](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#38)]  
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
