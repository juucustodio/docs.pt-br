---
description: 'Saiba mais sobre: execução remota vs. local'
title: Remoto vs. Execução de local
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ee50e943-9349-4c84-ab1c-c35d3ada1a9c
ms.openlocfilehash: ea4d85faedd4a299da292029e64d77132e1a65a9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695171"
---
# <a name="remote-vs-local-execution"></a>Remoto vs. Execução de local

Você pode decidir executando remotamente (isto é, o mecanismo de base de dados executa a consulta na base de dados) ou localmente suas consultas ([!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] executa a consulta em um cache local).  
  
## <a name="remote-execution"></a>Execução remoto  

 Considere a consulta a seguir:  
  
 [!code-csharp[DLinqQueryConcepts#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#7)]
 [!code-vb[DLinqQueryConcepts#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#7)]  
  
 Se seu base de dados tem milhares de linhas de pedidos, você não deseja recuperá-los todos para processar um subconjunto pequeno. Em [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], a classe de <xref:System.Data.Linq.EntitySet%601> implementa a interface de <xref:System.Linq.IQueryable> . Essa abordagem certifique-se de que essas consultas podem ser executadas remotamente. Dois benefícios principais fluem dessa técnica:  
  
- Os dados desnecessários não são recuperados.  
  
- Uma consulta executada pelo mecanismo de base de dados geralmente é mais eficiente devido aos índices de base de dados.  
  
## <a name="local-execution"></a>Execução local  

 Em outras situações, convém ter o conjunto completo de entidades relacionadas no cache local. Essa finalidade, <xref:System.Data.Linq.EntitySet%601> fornece o método de <xref:System.Data.Linq.EntitySet%601.Load%2A> para carregar explicitamente todos os membros de <xref:System.Data.Linq.EntitySet%601>.  
  
 Se <xref:System.Data.Linq.EntitySet%601> é carregado já, consultas subsequentes são executadas localmente. Essa abordagem ajuda em duas maneiras:  
  
- Se o conjunto completo deve ser usado localmente ou várias vezes, você pode evitar consultas e remotos latências associados.  
  
- A entidade pode ser serializada como uma entidade completo.  
  
 O fragmento de código a seguir ilustra como execução local pode ser obtida:  
  
 [!code-csharp[DLinqQueryConcepts#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#8)]
 [!code-vb[DLinqQueryConcepts#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#8)]  
  
## <a name="comparison"></a>Comparação  

 Esses dois recursos fornecem uma combinação eficiente de opções: execução remoto para grandes coleções e execução local para coleções pequenas ou onde a coleção completa é necessária. Você implementa a execução remoto com <xref:System.Linq.IQueryable>, e a execução local com uma coleção de memória de <xref:System.Collections.Generic.IEnumerable%601> . Para forçar a execução local (ou seja, <xref:System.Collections.Generic.IEnumerable%601> ), consulte [converter um tipo em um IEnumerable genérico](convert-a-type-to-a-generic-ienumerable.md).  
  
### <a name="queries-against-unordered-sets"></a>Consultas em conjuntos não ordenada  

 Observe a diferença importante entre uma coleção local que implementa <xref:System.Collections.Generic.List%601> e uma coleção que fornece consultas remotas executadas em relação a *conjuntos não ordenados* em um banco de dados relacional. os métodos de<xref:System.Collections.Generic.List%601> como aqueles que usam valores de índice requerem a semântica da lista, que normalmente não pode ser obtida com uma consulta remoto com um conjunto não ordenada. Por esse motivo, esses métodos carregam implicitamente <xref:System.Data.Linq.EntitySet%601> para permitir a execução local.  
  
## <a name="see-also"></a>Consulte também

- [Consulte conceitos](query-concepts.md)
