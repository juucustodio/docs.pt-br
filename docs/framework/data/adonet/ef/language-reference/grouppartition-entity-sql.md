---
description: 'Saiba mais sobre: GROUPPARTITION (Entity SQL)'
title: PARTIÇÃODOGRUPO (Entity SQL)
ms.date: 03/30/2017
ms.assetid: d0482e9b-086c-451c-9dfa-ccb024a9efb6
ms.openlocfilehash: 18fdb655f62f54d59c03c0a34f6f77c5ca26729e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696900"
---
# <a name="grouppartition-entity-sql"></a>PARTIÇÃODOGRUPO (Entity SQL)

Retorna uma coleção de valores de argumento que são projetados fora do partição atual do grupo que a agregação está relacionada. A agregação de `GroupPartition` é uma agregação grupo- base e não tem nenhum formulário coleção com base.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
GROUPPARTITION( [ALL|DISTINCT] expression )  
```  
  
## <a name="arguments"></a>Argumentos  

 `expression`  
 Qualquer expressão de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] .  
  
## <a name="remarks"></a>Comentários  

 A seguinte consulta gerencia uma lista de produtos e uma coleção de linha quantidades do pedido por cada produto:  
  
```sql  
SELECT p, GroupPartition(ol.Quantity) FROM LOB.OrderLines AS ol
  GROUP BY ol.Product AS p
```  
  
 As duas consultas são iguais semanticamente:  
  
```sql  
SELECT p, Sum(GroupPartition(ol.Quantity)) FROM LOB.OrderLines AS ol
  GROUP BY ol.Product AS p
SELET p, Sum(ol.Quantity) FROM LOB.OrderLines AS ol
  group by ol.Product as p  
```  
  
 O operador de `GROUPPARTITION` pode ser usado em conjunto com funções agregadas definidas pelo usuário.  
  
`GROUPPARTITION` é um operador aggregate especial que contém uma referência ao conjunto agrupado de entrada. Essa referência pode ser usada em qualquer lugar na consulta onde o PERTO GRUPO está no escopo. Por exemplo:
  
```sql  
SELECT p, GroupPartition(ol.Quantity) FROM LOB.OrderLines AS ol GROUP BY ol.Product AS p
```  
  
 Com um regular `GROUP BY` , os resultados do agrupamento ficam ocultos. Você pode usar os resultados em uma função agregada. Para ver os resultados de agrupamento, você precisa correlacionar os resultados de agrupamento e de entrada definidos usando um subconsulta. As duas consultas são equivalentes:  
  
```sql  
SELET p, (SELECT q FROM GroupPartition(ol.Quantity) AS q) FROM LOB.OrderLines AS ol GROUP BY ol.Product AS p
SELECT p, (SELECT ol.Quantity AS q FROM LOB.OrderLines AS ol2 WHERE ol2.Product = p) FROM LOB.OrderLines AS ol GROUP BY ol.Product AS p
```  
  
 Como mostrado no exemplo, o operador aggregate de GROUPPARTITION facilita obter uma referência a entrada definida após o agrupamento.  
  
 O operador GROUPPARTITION pode especificar qualquer [!INCLUDE[esql](../../../../../../includes/esql-md.md)] expressão na entrada do operador quando você usa o `expression` parâmetro.  
  
 Por exemplo todas as expressões da seguir de entrada a partição de grupo são válidas:  
  
```sql  
SELECT groupkey, GroupPartition(b) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey
SELECT groupkey, GroupPartition(1) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey
SELECT groupkey, GroupPartition(a + b) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey
SELECT groupkey, GroupPartition({a + b}) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey  
SELECT groupkey, GroupPartition({42}) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey  
SELECT groupkey, GroupPartition(b > a) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey  
```  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como usar a cláusula de GROUPPARTITION com o cláusula GROUP BY. O cláusula GROUP BY agrupa entidades de `SalesOrderHeader` pelo seu `Contact`. A cláusula de GROUPPARTITION projetos na propriedade de `TotalDue` para cada grupo, resultando em uma coleção de decimais.  
  
 [!code-sql[DP EntityServices Concepts#Collection_GroupPartition](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#collection_grouppartition)]
