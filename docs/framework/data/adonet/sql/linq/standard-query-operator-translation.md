---
description: 'Saiba mais sobre: tradução do operador de consulta padrão'
title: Conversão padrão de operador de consulta
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a60c30fa-1e68-45fe-b984-f6abb9ede40e
ms.openlocfilehash: e7e45e8f27f1e7d3c572f00ea014b4edb288b2b0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99681520"
---
# <a name="standard-query-operator-translation"></a>Conversão padrão de operador de consulta

O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] converte operadores de consulta padrão em comandos SQL. O processador de consulta do banco de dados determina a semântica de execução de conversão SQL.

Operadores de consulta padrão são definidos em *sequências*. Uma sequência é *ordenada* e depende da identidade de referência para cada elemento da sequência. Para obter mais informações, consulte Visão geral [dos operadores de consulta Standard (C#)](../../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md) ou [padrão de operadores de consulta (Visual Basic)](../../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md).

O SQL lida principalmente com *conjuntos de valores não ordenados*. A ordenação normalmente é indicada explicitamente, uma operação de pós-processamento que é aplicada ao resultado final de uma consulta em vez de aos resultados intermediários. A identidade é definida por valores. Por esse motivo, as consultas SQL são compreendidas para lidar com conjuntos de subconjuntos (*pacotes*) em vez de *conjuntos*.

Os parágrafos a seguir descrevem as diferenças entre os operadores de consulta padrão e sua conversão SQL do provedor SQL Server para [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].

## <a name="operator-support"></a>Suporte de operador

### <a name="concat"></a>Concat

O método <xref:System.Linq.Enumerable.Concat%2A> é definido para multisets ordenados onde a ordem do receptor e a ordem do argumento são as mesmas. O <xref:System.Linq.Enumerable.Concat%2A> funciona como `UNION ALL` sobre os multisets seguido pela ordem comum.

A etapa final é ordenar no SQL antes que os resultados sejam produzidos. O <xref:System.Linq.Enumerable.Concat%2A> não preserva a ordem de seus argumentos. Para garantir a ordem apropriada, você deve ordenar explicitamente os resultados de <xref:System.Linq.Enumerable.Concat%2A>.

### <a name="intersect-except-union"></a>Intersect, Except, Union

Os métodos <xref:System.Linq.Enumerable.Intersect%2A> e <xref:System.Linq.Enumerable.Except%2A> são bem-definidos somente em conjuntos. A semântica de multisets é indefinida.

O método <xref:System.Linq.Enumerable.Union%2A> é definido para multisets como a concatenação não ordenada dos multisets (efetivamente o resultado da cláusula UNION ALL no SQL).

### <a name="take-skip"></a>Take, Skip

<xref:System.Linq.Enumerable.Take%2A> os <xref:System.Linq.Enumerable.Skip%2A> métodos e são bem definidos somente em *conjuntos ordenados*. A semântica de conjuntos ou de multisets não ordenados é indefinida.

> [!NOTE]
> <xref:System.Linq.Enumerable.Take%2A> e <xref:System.Linq.Enumerable.Skip%2A> possuem certas limitações quando são usados em consultas no SQL Server 2000. Para obter mais informações, consulte a entrada "ignorar e considerar exceções no SQL Server 2000" em [solução de problemas](troubleshooting.md).

Devido a limitações na ordenação do SQL, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o tenta mover a ordenação do argumento desses métodos para o resultado do método. Por exemplo, considere a seguinte consulta [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]:

[!code-csharp[DLinqSQOTranslation#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#1)]
[!code-vb[DLinqSQOTranslation#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#1)]

O SQL gerado para esse código move a ordenação para o final, da seguinte maneira:

```sql
SELECT TOP 1 [t0].[CustomerID], [t0].[CompanyName],
FROM [Customers] AS [t0]
WHERE (NOT (EXISTS(
    SELECT NULL AS [EMPTY]
    FROM (
        SELECT TOP 1 [t1].[CustomerID]
        FROM [Customers] AS [t1]
        WHERE [t1].[City] = @p0
        ORDER BY [t1].[CustomerID]
        ) AS [t2]
    WHERE [t0].[CustomerID] = [t2].[CustomerID]
    ))) AND ([t0].[City] = @p1)
ORDER BY [t0].[CustomerID]
```

Torna-se óbvio que qualquer ordenação especificada precisa ser consistente quando <xref:System.Linq.Enumerable.Take%2A> e <xref:System.Linq.Enumerable.Skip%2A> são encadeados juntos. Caso contrário, os resultados serão indefinidos.

<xref:System.Linq.Enumerable.Take%2A> e <xref:System.Linq.Enumerable.Skip%2A> são definidos para argumentos inteiros não negativos, argumentos integrais constantes baseados na especificação de operador de consulta padrão.

### <a name="operators-with-no-translation"></a>Operadores sem a conversão

Os seguintes métodos não são convertidos pelo [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. O motivo mais comum é a diferença entre multisets e sequências não ordenados.

|Operadores|Fundamento|
|---------------|---------------|
|<xref:System.Linq.Enumerable.TakeWhile%2A>, <xref:System.Linq.Enumerable.SkipWhile%2A>|Consultas SQL operam em multisets, não em sequências. `ORDER BY` deve ser a última cláusula aplicada aos resultados. Por esse motivo, não há nenhuma conversão de finalidade geral para esses dois métodos.|
|<xref:System.Linq.Enumerable.Reverse%2A>|A conversão desse método é possível para um conjunto ordenado, mas, no momento, não é convertido pelo [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].|
|<xref:System.Linq.Enumerable.Last%2A>, <xref:System.Linq.Enumerable.LastOrDefault%2A>|A conversão desses métodos é possível para um conjunto ordenado, mas, no momento, não são convertidos pelo [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].|
|<xref:System.Linq.Enumerable.ElementAt%2A>, <xref:System.Linq.Enumerable.ElementAtOrDefault%2A>|As consultas SQL operam em multisets, não em sequências indexáveis.|
|<xref:System.Linq.Enumerable.DefaultIfEmpty%2A> (sobrecarga com arg padrão)|Em geral, um valor padrão não pode ser especificado para um tuple arbitrário. Valores nulos para tuples são possíveis em alguns casos com junções externas.|

## <a name="expression-translation"></a>Conversão de expressão

### <a name="null-semantics"></a>Semântica de nulo

O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não impõe semântica de comparação de nulo no SQL. Os operadores de comparação são convertidos sintaticamente para seus equivalentes SQL. Por esse motivo, a semântica reflete a semântica do SQL definida pelas configurações do servidor ou da conexão. Por exemplo, dois valores nulos são considerados diferentes sob as configurações padrão do SQL Server, mas você pode alterar as configurações para alterar a semântica. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não considera as configurações do servidor quando converte consultas.

Uma comparação com o nulo literal é convertida na versão apropriada do SQL (`is null` ou `is not null`).

O valor de `null` na ordenação é definido pelo SQL Server. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não altera a ordenação.

### <a name="aggregates"></a>Agregações

O método de agregação do operador de consulta padrão <xref:System.Linq.Enumerable.Sum%2A> avalia uma sequência vazia ou uma sequência que contém somente nulos como zero. No [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] , a semântica de SQL permanece inalterada e <xref:System.Linq.Enumerable.Sum%2A> é avaliada `null` em vez de zero para uma sequência vazia ou para uma sequência que contém somente valores nulos.

As limitações do SQL em resultados intermediários se aplicam às agregações no [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. As <xref:System.Linq.Enumerable.Sum%2A> quantidades de inteiros de 32 bits não são computadas usando resultados de 64 bits. Pode ocorrer estouro para uma [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tradução de <xref:System.Linq.Enumerable.Sum%2A> , mesmo que a implementação do operador de consulta padrão não cause um estouro para a sequência na memória correspondente.

Da mesma forma, a conversão de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] de valores inteiros do <xref:System.Linq.Enumerable.Average%2A> é computada como um `integer`, não como um `double`.

### <a name="entity-arguments"></a>Argumentos de entidade

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] habilita os tipos de entidade a serem usados <xref:System.Linq.Enumerable.GroupBy%2A> nos <xref:System.Linq.Enumerable.OrderBy%2A> métodos e. Na conversão desses operadores, o uso de um argumento de um tipo é considerado ser o equivalente a especificar todos os membros desse tipo. Por exemplo, o código a seguir é equivalente:

[!code-csharp[DLinqSQOTranslation#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#2)]
[!code-vb[DLinqSQOTranslation#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#2)]

### <a name="equatable--comparable-arguments"></a>Argumentos equitativos/comparáveis

A igualdade dos argumentos é necessária na implementação dos seguintes métodos:

- <xref:System.Linq.Enumerable.Contains%2A>

- <xref:System.Linq.Enumerable.Skip%2A>

- <xref:System.Linq.Enumerable.Union%2A>

- <xref:System.Linq.Enumerable.Intersect%2A>

- <xref:System.Linq.Enumerable.Except%2A>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dá suporte a igualdade e comparação para argumentos *simples* , mas não para argumentos que contenham sequências ou. Um argumento simples é um tipo que pode ser mapeado para uma linha SQL. Uma projeção de um ou mais tipos de entidade, que podem ser determinados estaticamente por não conterem uma sequência, é considerada um argumento simples.

Veja a seguir exemplos de argumentos simples:

[!code-csharp[DLinqSQOTranslation#3](~/samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#3)]
[!code-vb[DLinqSQOTranslation#3](~/samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#3)]

Veja a seguir exemplos de argumentos não-simples (hierárquicos):

[!code-csharp[DLinqSQOTranslation#4](~/samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#4)]
[!code-vb[DLinqSQOTranslation#4](~/samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#4)]

### <a name="visual-basic-function-translation"></a>Conversão de função do Visual Basic

As seguintes funções auxiliares que são usadas pelo compilador Visual Basic são convertidas em operadores e funções SQL correspondentes:

- `CompareString`

- `DateTime.Compare`

- `Decimal.Compare`

- `IIf (in Microsoft.VisualBasic.Interaction)`

Métodos de conversão:

|||||
|-|-|-|-|
|ToBoolean|ToSByte|ToByte|ToChar|
|ToCharArrayRankOne|ToDate|ToDecimal|ToDouble|
|ToInteger|ToUInteger|ToLong|ToULong|
|ToShort|ToUShort|ToSingle|ToString|

## <a name="inheritance-support"></a>Suporte à herança

### <a name="inheritance-mapping-restrictions"></a>Restrições de mapeamento de herança

Para obter mais informações, consulte [como mapear hierarquias de herança](how-to-map-inheritance-hierarchies.md).

### <a name="inheritance-in-queries"></a>Herança em consultas

As conversões do C# são suportadas apenas na projeção. Conversões que são usadas em outro lugar não são convertidas e são ignoradas. Com exceção dos nomes de funções SQL, o SQL realmente executa apenas o equivalente do <xref:System.Convert> do CLR (Common Language Runtime). Isto é, o SQL pode alterar o valor de um tipo para outro. Não há nenhum equivalente de conversão do CLR porque não há nenhum conceito de reinterpretação dos mesmos bits como os de outro tipo. É por isso que uma conversão C# funciona apenas localmente. Ela não funciona remotamente.

Os operadores `is` e `as` e o método `GetType` não são restritos ao operador `Select`. Podem ser usados em outros operadores de consulta também.

## <a name="sql-server-2008-support"></a>Suporte do SQL Server 2008

A partir do .NET Framework 3.5 SP1, o LINQ to SQL dá suporte ao mapeamento para novos tipos de data e hora introduzidos com o SQL Server 2008. Mas, há algumas limitações aos operadores de consulta do LINQ to SQL que você pode usar ao operar com valores mapeados para esses novos tipos.

### <a name="unsupported-query-operators"></a>Operadores de consulta não suportados

Os seguintes operadores de consulta não são suportados em valores mapeados para novos tipos de data e hora do SQL Server: `DATETIME2`, `DATE`, `TIME` e `DATETIMEOFFSET`.

- `Aggregate`

- `Average`

- `LastOrDefault`

- `OfType`

- `Sum`

Para obter mais informações sobre mapeamento para esses SQL Server tipos de data e hora, consulte [mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md).

## <a name="sql-server-2005-support"></a>Suporte do SQL Server 2005

O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não dá suporte aos seguintes recursos do SQL Server 2005:

- Procedimentos armazenados escritos para SQL CLR.

- Tipo definido pelo usuário.

- Recursos de consulta XML.

## <a name="sql-server-2000-support"></a>Suporte do SQL Server 2000

As limitações a seguir SQL Server 2000 (em comparação com Microsoft SQL Server 2005) afetam o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] suporte.

### <a name="cross-apply-and-outer-apply-operators"></a>Operadores Cross Apply e Outer Apply

Esses operadores não estão disponíveis no SQL Server 2000. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tenta uma série de reescritas para substituí-los com junções apropriadas.

O `Cross Apply` e o `Outer Apply` são gerados para navegações de relacionamento. O conjunto de consultas para as quais essas reescritas são possíveis não é bem definido. Por esse motivo, o conjunto mínimo de consultas com suporte para SQL Server 2000 é o conjunto que não envolve a navegação de relação.

### <a name="text--ntext"></a>text/ntext

Os tipos `text`  /  `ntext` de dados não podem ser usados em determinadas operações de consulta `varchar(max)`  /  `nvarchar(max)` , que têm suporte do Microsoft SQL Server 2005.

Nenhuma resolução está disponível para essa limitação. Especificamente, você não pode usar `Distinct()` em resultados que contêm membros que são mapeados para colunas `text` ou `ntext`.

### <a name="behavior-triggered-by-nested-queries"></a>Comportamento disparado por consultas aninhadas

SQL Server o associador 2000 (por meio do SP4) tem algumas idiossincrasias disparadas por consultas aninhadas. O conjunto de consultas SQL que dispara essas idiossincrasias não é bem definido. Por esse motivo, você não pode definir o conjunto de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] consultas que podem causar SQL Server exceções.

### <a name="skip-and-take-operators"></a>Operadores Skip e Take

<xref:System.Linq.Enumerable.Take%2A> e <xref:System.Linq.Enumerable.Skip%2A> possuem certas limitações quando são usados em consultas no SQL Server 2000. Para obter mais informações, consulte a entrada "ignorar e considerar exceções no SQL Server 2000" em [solução de problemas](troubleshooting.md).

## <a name="object-materialization"></a>Materialização de objetos

A materialização cria objetos CLR das linhas que são retornadas por uma ou mais consultas SQL.

- As seguintes chamadas são *executadas localmente* como parte da materialização:

  - Construtores

  - Métodos `ToString` em projeções

  - Conversões de tipos em projeções

- Os métodos que seguem o <xref:System.Linq.Enumerable.AsEnumerable%2A> método são *executados localmente*. Esse método não provoca uma execução imediata.

- Você pode usar `struct` como o tipo de retorno de um resultado de consulta ou como um membro do tipo de resultado. As entidades precisam ser classes. Tipos anônimos são materializados como instâncias de classe, mas structs nomeados (não entidades) podem ser usados na projeção.

- Um membro do tipo do retorno de um resultado de consulta pode ser do tipo <xref:System.Linq.IQueryable%601>. É materializado como uma coleção local.

- Os métodos a seguir causam a *materialização imediata* da sequência à qual os métodos são aplicados:

  - <xref:System.Linq.Enumerable.ToList%2A>

  - <xref:System.Linq.Enumerable.ToDictionary%2A>

  - <xref:System.Linq.Enumerable.ToArray%2A>

## <a name="see-also"></a>Consulte também

- [Referência](reference.md)
- [Elementos Return ou Skip em uma sequência](return-or-skip-elements-in-a-sequence.md)
- [Concatenar duas sequências](concatenate-two-sequences.md)
- [Retornar a diferença entre duas sequências ajustada](return-the-set-difference-between-two-sequences.md)
- [Retornar a interseção de sequências de duas](return-the-set-intersection-of-two-sequences.md)
- [Retornar a união de sequências de duas](return-the-set-union-of-two-sequences.md)
