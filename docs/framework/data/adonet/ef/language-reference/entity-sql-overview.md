---
description: 'Saiba mais sobre: Entity SQL visão geral'
title: Visão geral da Entity SQL
ms.date: 03/30/2017
ms.assetid: f0bb8120-e709-40a3-ac1e-5520dc47477d
ms.openlocfilehash: eb337ff3894b24d787d829838c9cf12c934a823c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724603"
---
# <a name="entity-sql-overview"></a>Visão geral da Entity SQL

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] é uma linguagem semelhante a SQL que permite consultar modelos conceituais na Entity Framework. Os modelos conceituais representam dados como entidades e relações e [!INCLUDE[esql](../../../../../../includes/esql-md.md)] permitem que você consulte essas entidades e relações em um formato familiar para aqueles que usaram o SQL.  

 O Entity Framework funciona com provedores de dados específicos de armazenamento para converter generic [!INCLUDE[esql](../../../../../../includes/esql-md.md)] em consultas específicas de armazenamento. O provedor EntityClient permite executar um comando [!INCLUDE[esql](../../../../../../includes/esql-md.md)] em um modelo de entidade e retornar tipos de dados ricos que incluem resultados escalares, conjuntos de resultados e gráficos de objeto. Ao criar objetos <xref:System.Data.EntityClient.EntityCommand>, você pode especificar um nome de procedimento armazenado ou o texto de uma consulta atribuindo uma cadeia de caracteres de consulta [!INCLUDE[esql](../../../../../../includes/esql-md.md)] a sua propriedade <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType>. O <xref:System.Data.EntityClient.EntityDataReader> expõe os resultados da execução de um <xref:System.Data.EntityClient.EntityCommand> em um EDM. Para executar o comando que retorna <xref:System.Data.EntityClient.EntityDataReader>, chame <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>.  
  
 Além do provedor EntityClient, o Entity Framework permite que você use o [!INCLUDE[esql](../../../../../../includes/esql-md.md)] para executar consultas em um modelo conceitual e retornar dados como objetos CLR fortemente tipados que são instâncias de tipos de entidade. Para obter mais informações, consulte [trabalhando com objetos](../working-with-objects.md).  
  
 Esta seção fornece informações conceituais sobre a linguagem [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  

 [Como o Entity SQL difere do Transact-SQL](how-entity-sql-differs-from-transact-sql.md)  
  
 [Referência rápida de Entity SQL](entity-sql-quick-reference.md)  
  
 [Sistema de tipo](type-system-entity-sql.md)  
  
 [Definições de tipo](type-definitions-entity-sql.md)  
  
 [Construir tipos](constructing-types-entity-sql.md)  
  
 [Cache de plano de consulta](query-plan-caching-entity-sql.md)  
  
 [Namespaces](namespaces-entity-sql.md)  
  
 [Identificadores](identifiers-entity-sql.md)  
  
 [Parâmetros](parameters-entity-sql.md)  
  
 [Variáveis](variables-entity-sql.md)  
  
 [Expressões sem suporte](unsupported-expressions-entity-sql.md)  
  
 [Literais](literals-entity-sql.md)  
  
 [Literais nulos e inferência de tipos](null-literals-and-type-inference-entity-sql.md)  
  
 [Conjunto de caracteres de entrada](input-character-set-entity-sql.md)  
  
 [Expressões de consulta](query-expressions-entity-sql.md)  
  
 [Funções](functions-entity-sql.md)  
  
 [Precedência de operador](operator-precedence-entity-sql.md)  
  
 [Houver](paging-entity-sql.md)  
  
 [Semântica de comparação](comparison-semantics-entity-sql.md)  
  
 [Composta consultas aninhadas Entity SQL](composing-nested-entity-sql-queries.md)  
  
 [Tipos estruturados que permitem valor nulo](nullable-structured-types-entity-sql.md)  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Linguagem Entity SQL](entity-sql-language.md)
- [Especificações de CSDL, SSDL e MSL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
