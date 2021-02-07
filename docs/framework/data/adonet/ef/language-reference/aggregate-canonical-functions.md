---
description: 'Saiba mais sobre: agregar funções canônicas'
title: Funções agregadas canônicas
ms.date: 03/30/2017
ms.assetid: 3bcff826-ca90-41b3-a791-04d6ff0e5085
ms.openlocfilehash: e26888ac15553a592f7d2cb9b1a0941161115615
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99697290"
---
# <a name="aggregate-canonical-functions"></a>Funções agregadas canônicas

Agregados são as expressões em que reduz uma série de valores de entrada, por exemplo, um único valor. Agregados são normalmente usadas em conjunto com o cláusula GROUP BY de expressão SELECT, e há restrições em onde eles podem ser usados.

## <a name="aggregate-entity-sql-canonical-functions"></a>Funções de agregação Entity SQL canônicas

Veja a seguir a agregação Entity SQL funções canônicas.

### <a name="avgexpression"></a>Avg (expressão)

Retorna a média dos valores não anuláveis.

**Argumentos**

Um `Int32` , `Int64` , `Double` e `Decimal` .

**Valor retornado**

O tipo de `expression` , ou `null` se todos os valores de entrada forem `null` valores.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_AVG](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_avg)]
[!code-sql[DP EntityServices Concepts#EDM_AVG](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_avg)]

### <a name="bigcountexpression"></a>BigCount (expressão)

Retorna o tamanho do agregado que inclui valores nulos e duplicados.

**Argumentos**

Qualquer tipo.

**Valor retornado**

Um `Int64`.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_BIGCOUNT](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_bigcount)]
[!code-sql[DP EntityServices Concepts#EDM_BIGCOUNT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_bigcount)]

### <a name="countexpression"></a>Contagem (expressão)

Retorna o tamanho do agregado que inclui valores nulos e duplicados.

**Argumentos**

Qualquer tipo.

**Valor retornado**

Um `Int32`.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_COUNT](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_count)]
[!code-sql[DP EntityServices Concepts#EDM_COUNT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_count)]

### <a name="maxexpression"></a>Máximo (expressão)

Retorna o máximo dos valores não anuláveis.

**Argumentos**

`Byte`, `Int16`, `Int32`, `Int64`, `Byte`, `Single`, `Double`, `Decimal`, `DateTime`, `DateTimeOffset`, `Time`, `String`, `Binary`.

**Valor retornado**

O tipo de `expression` , ou `null` se todos os valores de entrada forem `null` valores.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_MAX](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_max)]
[!code-sql[DP EntityServices Concepts#EDM_MAX](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_max)]

### <a name="minexpression"></a>Minuto (expressão)

Retorna o mínimo dos valores não anuláveis.

**Argumentos**

`Byte`, `Int16`, `Int32`, `Int64`, `Byte`, `Single`, `Double`, `Decimal`, `DateTime`, `DateTimeOffset`, `Time`, `String`, `Binary`.

**Valor retornado**

O tipo de `expression` , ou `null` se todos os valores de entrada forem `null` valores.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_MIN](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_min)]
[!code-sql[DP EntityServices Concepts#EDM_MIN](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_min)]

### <a name="stdevexpression"></a>StDev (expressão)

Retorna o desvio padrão de valores não anuláveis.

**Argumentos**

`Int32`, `Int64`, `Double`, `Decimal`.

**Valor retornado**

Um `Double`. `Null`, se todos os valores de entrada são valores de `null` .

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_STDEV](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_stdev)]
[!code-sql[DP EntityServices Concepts#EDM_STDEV](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_stdev)]

### <a name="stdevpexpression"></a>StDevP (expressão)

Retorna o desvio padrão para a população de todos os valores.

**Argumentos**

`Int32`, `Int64`, `Double`, `Decimal`.

**Valor retornado**

Um `Double` , ou `null` se todos os valores de entrada forem `null` valores.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_STDEVP](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_stdevp)]
[!code-sql[DP EntityServices Concepts#EDM_STDEVP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_stdevp)]

### <a name="sumexpression"></a>Soma (expressão)

Retorna a soma dos valores não anuláveis.

**Argumentos**

`Int32`, `Int64`, `Double`, `Decimal`.

**Valor retornado**

Um `Double` , ou `null` se todos os valores de entrada forem `null` valores.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_SUM](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_sum)]
[!code-sql[DP EntityServices Concepts#EDM_SUM](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_sum)]

### <a name="varexpression"></a>Var (expressão)

Retorna a variação de todos os valores não anuláveis.

**Argumentos**

`Int32`, `Int64`, `Double`, `Decimal`.

**Valor retornado**

Um `Double` , ou `null` se todos os valores de entrada forem `null` valores.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_VAR](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_var)]
[!code-sql[DP EntityServices Concepts#EDM_VAR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_var)]

### <a name="varpexpression"></a>VarP (expressão)

Retorna a variação para a população de todos os valores não anuláveis.

**Argumentos**

`Int32`, `Int64`, `Double`, `Decimal`.

**Valor retornado**

Um `Double` , ou `null` se todos os valores de entrada forem `null` valores.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_VARP](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_varp)]
[!code-sql[DP EntityServices Concepts#EDM_VARP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_varp)]

Funcionalidade equivalente está disponível no provedor gerenciado cliente do Microsoft SQL. Para obter mais informações, consulte [SqlClient para funções de Entity Framework](../sqlclient-for-ef-functions.md).

## <a name="collection-based-aggregates"></a>Agregações baseadas em coleção

Agregados coleção com base (funções de coleção) operam em coleções e retornam um valor. Por exemplo, se ORDERs for uma coleção de todos os pedidos, você poderá calcular a data de remessa mais antiga com a seguinte expressão:

```sql
min(select value o.ShipDate from LOB.Orders as o)
```

Agregados coleções baseadas dentro de expressões são avaliadas dentro do escopo ambiente atual de resolução.

## <a name="group-based-aggregates"></a>Agregações baseadas em grupo

Agregados Grupo- com base são calculadas sobre um grupo como definidas por cláusula GROUP BY. Para cada grupo em resultado, uma agregação separada é calculada usando elementos em cada grupo como entrada ao cálculo agregado. Quando a grupo- pela cláusula é usado em uma expressão selecionar, simplesmente agrupamento nomes de expressão, agregados, ou expressões constantes podem acessar estar presente na projeção ou ordem- pela cláusula.

O exemplo a seguir calcula a média quantidade ordenada para cada produto:

```sql
select p, avg(ol.Quantity) from LOB.OrderLines as ol
  group by ol.Product as p
```

É possível ter uma agregação baseada em grupo sem uma cláusula Group by explícita na expressão SELECT. Nesse caso, todos os elementos são tratados como um único grupo. Isso é equivalente a especificar um agrupamento com base em uma constante. Tomada, por exemplo, a expressão a seguir:

```sql
select avg(ol.Quantity) from LOB.OrderLines as ol
```

Isso é equivalente ao seguinte:

```sql
select avg(ol.Quantity) from LOB.OrderLines as ol group by 1
```

As expressões na agregação grupo- base são avaliadas dentro do escopo de resolução que seria visível para a cláusula WHERE expressão.

Como no Transact-SQL, agregações baseadas em grupo também podem especificar um modificador ALL ou DISTINCT. Se o modificador DISTINCT é especificado, as duplicatas são eliminadas de coleção de entrada aggregate, antes que a agregação é calculada apenas. Se TODOS OS modificador é especificado (ou se nenhum modificador é especificado), nenhuma descarte duplicado é executada.

## <a name="see-also"></a>Consulte também

- [Funções canônicas](canonical-functions.md)
