---
title: LINHA (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 06da96e8-55d7-486c-991a-4e514d837ff9
ms.openlocfilehash: 4fb16fe0072066580bff36ac0879ff38217f1e34
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319384"
---
# <a name="row-entity-sql"></a>LINHA (Entity SQL)
Constrói registros anônimos e tipados estruturalmente de um ou mais valores.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
ROW ( expression [ AS alias ] [,...] )  
```  
  
## <a name="arguments"></a>Arguments  
 `expression`  
 Qualquer expressão de consulta válida que retorna um valor para construir em seguida o tipo.  
  
 `alias`  
 Especifica um alias para uma linha no tipo especificado valor. Se um alias não for fornecido, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tentará gerar um alias com base nas regras de geração de alias [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
## <a name="return-value"></a>Valor retornado  
 Um tipo de linha.  
  
## <a name="remarks"></a>Comentários  
 Você usa construtores de linha no [!INCLUDE[esql](../../../../../../includes/esql-md.md)] para construir registros anônimos e tipados de forma estrutural a partir de um ou mais valores. O tipo do resultado de um construtor de linha é um tipo de linha cujos tipos de campo correspondem aos tipos de valores que foram usados para construir a linha. Por exemplo, a expressão a seguir constrói um valor do tipo `Record(a int, b string, c int)`.  
  
```sql  
ROW(1 AS a, "abc" AS b, a+34 AS c)  
```  
  
 Se você não fornecer um alias para um construtor de expressão em seguida, Entity Framework tentará gerar um. Para obter mais informações, consulte a seção "regras de alias" do tópico [identificadores](identifiers-entity-sql.md) .  
  
 As seguintes regras se aplicam para o construtor de serrilha de expressão em uma linha:  
  
- O construtor das expressões em uma linha não pode referenciar outras alias no mesmo construtor.  
  
- Duas expressões no mesmo construtor de linha não podem ter as mesmas alias.  
  
 Para obter mais informações sobre construtores de consulta, consulte [construindo tipos](constructing-types-entity-sql.md).  
  
## <a name="example"></a>Exemplo  
 A seguinte consulta SQL Entity usa o operador de LINHA para construir registros anônimos, estrutural tipados. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#ROW](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#row)]  
  
## <a name="see-also"></a>Consulte também

- [Construindo tipos](constructing-types-entity-sql.md)
- [Referência de Entity SQL](entity-sql-reference.md)
- [Definições de tipo](type-definitions-entity-sql.md)
