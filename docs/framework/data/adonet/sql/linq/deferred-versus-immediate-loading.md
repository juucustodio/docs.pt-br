---
description: 'Saiba mais sobre: carregamento retardado versus imediato'
title: Adiado contra a carga immediate
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1d7247f-a3b7-460b-b342-5c1a2365aa1a
ms.openlocfilehash: 8c2237bd726ca79c7c168040e2a701f51ec3d238
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100464749"
---
# <a name="deferred-versus-immediate-loading"></a>Adiado contra a carga immediate

Quando você consulta para um objeto, você só retorna o objeto que você solicitou. Os objetos *relacionados* não são buscados automaticamente ao mesmo tempo. (Para obter mais informações, consulte [consultando entre relações](querying-across-relationships.md).) Você não pode ver o fato de que os objetos relacionados ainda não foram carregados, pois uma tentativa de acessá-los produz uma solicitação que os recupera.  
  
 Por exemplo, talvez você queira consultar um determinado conjunto de pedidos e, ocasionalmente, enviar uma notificação por email a clientes específicos. Você não precisará necessariamente inicialmente de recuperar todos os dados do cliente com cada pedido. Você pode usar o carregamento adiada para adiar a recuperação de informações extras até que você tenha que absolutamente. Considere o seguinte exemplo:  
  
 [!code-csharp[DLinqQueryConcepts#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#1)]
 [!code-vb[DLinqQueryConcepts#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#1)]  
  
 O oposto também pode ser true. Você pode ter um aplicativo que tenha que exibir o cliente e ordenação dados ao mesmo tempo. Você conhece-o necessidade dois conjuntos de dados. Você sabe suas informações de ordem das necessidades do aplicativo para cada cliente para que você obter os resultados. Você não deve enviar para consultas individuais de pedidos para cada cliente. O que você deseja realmente é recuperar os dados de pedidos juntamente com os clientes.  
  
 [!code-csharp[DLinqQueryConcepts#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#2)]
 [!code-vb[DLinqQueryConcepts#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#2)]  
  
 Você também pode associar à clientes e pedidos em uma consulta formando entre o produto e recuperar todos os bits de dados relacionados como uma grande projeção. Mas esses resultados não são entidades. (Para obter mais informações, consulte [o modelo de objeto LINQ to SQL](the-linq-to-sql-object-model.md)). As entidades são objetos que possuem a identidade e que você pode alterar, enquanto esses resultados seriam as projeções que não podem ser modificadas e persistente. Ainda pior, você poderia ser recuperando lotes de dados redundantes como as repetições de cada cliente para cada ordem em aplainado se associam a saída.  
  
 O que você precisa realmente é uma maneira para recuperar ao mesmo tempo um conjunto de objetos relacionados. O conjunto é uma seção delineado de um gráfico de modo que você nunca está recuperando mais ou menos que foi necessário para seu uso pretendido. Para essa finalidade, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fornece o <xref:System.Data.Linq.DataLoadOptions> carregamento imediato de uma região do modelo de objeto. Os métodos incluem:  
  
- O método de <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> , imediatamente para carregar os dados relacionados ao destino principal.  
  
- O método de <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> , para filtrar os objetos recuperados para um relacionamento específico.  
  
## <a name="see-also"></a>Consulte também

- [Consulte conceitos](query-concepts.md)
