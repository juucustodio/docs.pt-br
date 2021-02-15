---
description: 'Saiba mais sobre: formular junções e consultas entre produtos'
title: Formular junções e consultas entre produtos
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d8072ede-0521-4670-9bec-1778ceeb875b
ms.openlocfilehash: 1adee3576d7b30d6ec9a9c4e920befcd21dd9e85
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739112"
---
# <a name="formulate-joins-and-cross-product-queries"></a>Formular junções e consultas entre produtos

Os exemplos a seguir mostram como combinar resultados de várias tabelas.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a navegação de chave estrangeira na `From` cláusula em Visual Basic ( `from` cláusula em C#) para selecionar todos os pedidos de clientes em Londres.  
  
 [!code-csharp[DLinqQueryExamples#47](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#47)]
 [!code-vb[DLinqQueryExamples#47](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#47)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a navegação de chave estrangeira na `Where` cláusula em Visual Basic ( `where` cláusula em C#) para filtrar por indisponibilidade de estoque `Products` cujo `Supplier` está na Estados Unidos.  
  
 [!code-csharp[DLinqQueryExamples#48](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#48)]
 [!code-vb[DLinqQueryExamples#48](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#48)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a navegação de chave estrangeira na `From` cláusula em Visual Basic ( `from` cláusula em C#) para filtrar os funcionários em Seattle e listar seus territórios.  
  
 [!code-csharp[DLinqQueryExamples#49](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#49)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a navegação de chave estrangeira na `Select` cláusula em Visual Basic ( `select` cláusula em C#) para filtrar os pares de funcionários em que um funcionário se reporta ao outro e onde ambos os funcionários são do mesmo `City` .  
  
 [!code-csharp[DLinqQueryExamples#50](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#50)]
 [!code-vb[DLinqQueryExamples#50](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#50)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir Visual Basic procura todos os clientes e pedidos, garante que os pedidos sejam correspondidos aos clientes e garante que, para cada cliente nessa lista, um nome de contato seja fornecido.  
  
 [!code-vb[DLinqQueryExamples#50v](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#50v)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir une explicitamente duas tabelas e os resultados dos projetos das duas tabelas.  
  
 [!code-csharp[DLinqQueryExamples#51](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#51)]
 [!code-vb[DLinqQueryExamples#51](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#51)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir une explicitamente três tabelas e os resultados dos projetos de cada uma delas.  
  
 [!code-csharp[DLinqQueryExamples#52](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#52)]
 [!code-vb[DLinqQueryExamples#52](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#52)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como obter um `LEFT OUTER JOIN` usando `DefaultIfEmpty()`. O método `DefaultIfEmpty()` retorna nulo quando não há nenhum `Order` para o `Employee`.  
  
 [!code-csharp[DLinqQueryExamples#53](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#53)]
 [!code-vb[DLinqQueryExamples#53](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#53)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir projeta uma expressão `let` resultante de uma junção.  
  
 [!code-csharp[DLinqQueryExamples#54](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#54)]
 [!code-vb[DLinqQueryExamples#54](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#54)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra um `join` com uma chave composta.  
  
 [!code-csharp[DLinqQueryExamples#55](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#55)]
 [!code-vb[DLinqQueryExamples#55](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#55)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como construir um `join` onde um lado é anulável e o outro não.  
  
 [!code-csharp[DLinqQueryExamples#56](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#56)]
 [!code-vb[DLinqQueryExamples#56](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#56)]  
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
