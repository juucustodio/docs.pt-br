---
description: 'Saiba mais sobre: operações do quantificador (Visual Basic)'
title: Operações de quantificador
ms.date: 07/20/2015
ms.assetid: ae1a2b73-503c-4f4b-a3fd-31b5adbee67c
ms.openlocfilehash: 7cbd8a9cf18a0ad8b70ada58d7fa6602dce4bd1b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100430086"
---
# <a name="quantifier-operations-visual-basic"></a>Operações do quantificador (Visual Basic)

As operações de quantificador retornam um valor <xref:System.Boolean> que indica se alguns ou todos os elementos em uma sequência satisfazem uma condição.  
  
 A ilustração a seguir mostra duas operações de quantificador diferentes em duas sequências de origem diferentes. A primeira operação pergunta se um ou mais dos elementos são o caractere 'A' e o resultado é `true`. A segunda operação pergunta se todos os elementos são o caractere 'A' e o resultado é `true`.  
  
 ![Operações de quantificador LINQ](./media/quantifier-operations/linq-quantifier-operations.png)  
  
 Os métodos de operador de consulta padrão que realizam operações de quantificador estão listados na seção a seguir.  
  
## <a name="methods"></a>Métodos  
  
|Nome do método|Descrição|Visual Basic sintaxe de expressão de consulta|Mais informações|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|Todos|Determina se todos os elementos em uma sequência satisfazem uma condição.|`Aggregate … In … Into All(…)`|<xref:System.Linq.Enumerable.All%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.All%2A?displayProperty=nameWithType>|  
|Qualquer|Determina se todos os elementos em uma sequência satisfazem uma condição.|`Aggregate … In … Into Any()`|<xref:System.Linq.Enumerable.Any%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Any%2A?displayProperty=nameWithType>|  
|Contém|Determina se uma sequência contém um elemento especificado.|Não aplicável.|<xref:System.Linq.Enumerable.Contains%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Contains%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-examples"></a>Exemplos de sintaxe de expressão de consulta  

 Esses exemplos usam a `Aggregate` cláusula em Visual Basic como parte da condição de filtragem em uma consulta LINQ.  
  
 O exemplo a seguir usa a `Aggregate` cláusula e o <xref:System.Linq.Enumerable.All%2A> método de extensão para retornar de uma coleção as pessoas cujos animais de estimação são todos mais antigos do que uma idade especificada.  
  
 [!code-vb[CsLINQAnyAll#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAnyAll/VB/AnyAll.vb#1)]  
  
 O exemplo a seguir usa a `Aggregate` cláusula e o <xref:System.Linq.Enumerable.Any%2A> método de extensão para retornar de uma coleção as pessoas que têm pelo menos um animal de estimação que seja mais antigo que uma idade especificada.  
  
 [!code-vb[CsLINQAnyAll#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAnyAll/VB/AnyAll.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Linq>
- [Visão geral de operadores de consulta padrão (Visual Basic)](standard-query-operators-overview.md)
- [Cláusula Aggregate](../../../language-reference/queries/aggregate-clause.md)
- [Como consultar frases que contêm um conjunto especificado de palavras (LINQ) (Visual Basic)](how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)
