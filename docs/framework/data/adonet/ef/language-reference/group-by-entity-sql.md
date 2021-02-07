---
description: 'Saiba mais sobre: agrupar por (Entity SQL)'
title: AGRUPAR POR (Entity SQL)
ms.date: 03/30/2017
ms.assetid: cf4f4972-4724-4945-ba44-943a08549139
ms.openlocfilehash: 16328b46a59a2a07622cda43dce30d8b4f1d3dde
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696926"
---
# <a name="group-by-entity-sql"></a>AGRUPAR POR (Entity SQL)

Especifica os grupos nos quais os objetos retornados por uma expressão de consulta ([Select](select-entity-sql.md)) devem ser colocados.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
[ GROUP BY aliasedExpression [ ,...n ] ]  
```  
  
## <a name="arguments"></a>Argumentos  

 `aliasedExpression`  
 Qualquer expressão de consulta válida em que o agrupamento for executado. `expression` pode ser uma propriedade ou uma expressão de não agregação que referencia uma propriedade retornada pela cláusula. Cada expressão em um cláusula GROUP BY deve ser avaliada como um tipo que pode ser comparado para igualdade. Esses tipos são geralmente primitivos escalares como números, cadeias de caracteres, e datas. Você não pode agrupar por uma coleção.  
  
## <a name="remarks"></a>Comentários  

 Se as funções de agregação forem incluídas na cláusula SELECT \<select list> , Group by calculará um valor de resumo para cada grupo. Quando o GRUPO é especificado PERTO, ou cada nome de propriedade em qualquer expressão de nonaggregate na lista select deve ser incluído na lista GRUPO, ou o GROUP BY expressão deve coincidir exatamente com a expressão selecionar a lista.  
  
> [!NOTE]
> Se a cláusula ORDER BY não for especificado, os grupos retornados pelo cláusula GROUP BY não estão em qualquer ordem específica. Para especificar ordem específica de dados, nós recomendamos que você sempre use a cláusula ORDER BY.  
  
 Quando um cláusula GROUP BY é especificado, explícita ou implicitamente (por exemplo, a cláusula HAVING na consulta), o escopo atual está oculto, e um novo escopo é apresentado.  
  
 A cláusula SELECT, a cláusula HAVING, e a cláusula GROUP BY não poderão consultar os nomes de elemento especificado na cláusula. Você só pode usar expressões elas mesmas de agrupamento. Para fazer isso, você pode atribuir novos nomes (alias) para cada expressão de agrupamento. Se nenhum alias for especificada para uma expressão de agrupamento, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tenta gerar um usando as regras de geração de alias, conforme ilustrado no exemplo a seguir.  
  
 `SELECT g1, g2, ...gn FROM c as c1`  
  
 `GROUP BY e1 as g1, e2 as g2, ...en as gn`  
  
 As expressões em cláusula GROUP BY não podem referir-se nomes definidos anteriormente no mesmo cláusula GROUP BY.  
  
 Além de nomes de agrupamento, você também pode especificar agregados na cláusula SELECT, TENDO a cláusula, e a cláusula GROUP BY. Uma agregação contém uma expressão que é avaliada para cada elemento de grupo. O operador aggregate reduz os valores de todas essas expressões (normalmente, mas nem sempre, em um único valor.) A expressão aggregate pode fazer referências aos nomes de elementos visíveis originais no escopo pai, ou a alguns dos novos nomes introduzidos por cláusula GROUP BY próprio. Embora as agregações apareçam na cláusula SELECT, TENDO a cláusula, e a cláusula GROUP BY, são avaliadas realmente no mesmo escopo que as expressões de agrupamento, conforme ilustrado no exemplo a seguir.  
  
 `SELECT name, sum(o.Price * o.Quantity) as total`  
  
 `FROM orderLines as o`  
  
 `GROUP BY o.Product as name`  
  
 Esta consulta usa o cláusula GROUP BY para gerar um relatório de custo de todos os produtos ordenados, subproduto dividido. Ele fornece o nome `name` para o produto como parte da expressão de agrupamento e, em seguida, faz referência a esse nome na lista de seleção. Ele também especifica a agregação `sum` na lista de seleção que faz referência interna ao preço e à quantidade da linha de ordem.  
  
 Cada GROUP BY expressão chave deve ter pelo menos uma referência ao escopo de entrada:  
  
```sql  
SELECT FROM Persons as P  
GROUP BY Q + P   -- GOOD  
GROUP BY Q   -- BAD  
GROUP BY 1   -- BAD, a constant is not allowed  
```  
  
 Para obter um exemplo de como usar GROUP BY, consulte [tendo](having-entity-sql.md).  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta SQL Entity usa o GRUPO pelo operador para especificar os grupos em que os objetos são retornados por uma consulta. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna os resultados de primitivatype](../how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecutePrimitiveTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#GROUPBY](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#groupby)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Expressões de consulta](query-expressions-entity-sql.md)
