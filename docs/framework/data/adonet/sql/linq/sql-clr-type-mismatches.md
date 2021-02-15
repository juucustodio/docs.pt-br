---
description: 'Saiba mais sobre: incompatibilidades de tipo SQL-CLR'
title: Incompatibilidade de SQL-CLR
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0a90c33f-7ed7-4501-ad5f-6224c5da8e9b
ms.openlocfilehash: 9a2e1d360fc2a54f401572e46d92654f2b9284db
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803718"
---
# <a name="sql-clr-type-mismatches"></a>Incompatibilidade de SQL-CLR

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] automatiza muitas de conversão entre o modelo de objeto e o SQL Server. Entretanto, algumas situações impedem a conversão exata. Essas incompatíveis chave entre Common Language Runtime (CLR) tipo e os tipos de base de dados do SQL Server são resumidas nas seções a seguir. Você pode encontrar mais detalhes sobre mapeamentos de tipo específicos e conversão de função em [tipos de dados e funções](data-types-and-functions.md)de [mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md) .

## <a name="data-types"></a>Tipos de dados

A conversão entre CLR SQL Server e ocorre quando uma consulta está sendo enviadas a base de dados, e quando os resultados são novamente enviado ao seu modelo de objeto. Por exemplo, a seguinte consulta de Transact-SQL requer duas conversões de valor:

```sql
Select DateOfBirth From Customer Where CustomerId = @id
```

Antes que a consulta pode ser executada no SQL Server, o valor para o parâmetro de Transact-SQL deve ser especificado. Nesse exemplo, o valor do parâmetro de `id` deve primeiro ser convertido de um tipo de CLR <xref:System.Int32?displayProperty=nameWithType> a um tipo SQL Server `INT` de modo que a base de dados pode compreender o que o valor é. Para recuperar os resultados, a coluna SQL Server `DateOfBirth` deve ser convertido de um tipo SQL Server `DATETIME` a um tipo de CLR <xref:System.DateTime?displayProperty=nameWithType> para uso no modelo de objeto. Nesse exemplo, os tipos no modelo de objeto CLR e na base de dados SQL Server têm mapeamentos naturais. Mas, isto não é sempre o caso.

### <a name="missing-counterparts"></a>Contrapartes ausentes

Os seguintes tipos não têm correspondentes razoáveis.

- Incompatíveis no namespace de CLR <xref:System> :

  - **Inteiros não assinados**. Esses tipos são mapeados normalmente a suas contrapartes assinados de tamanho maior para evitar estouro. Literais podem ser convertidos em um sinal numérico do mesmo ou de menor tamanho, com base no valor.

  - **Boolean**. Esses tipos podem ser mapeados para um bit ou um número maior ou uma cadeia de caracteres. Um literal pode ser mapeado para uma expressão que avalia para o mesmo valor (por exemplo, `1=1` em SQL para `True` em CLS).

  - **TimeSpan**. Este tipo representa a diferença entre dois valores de `DateTime` e não corresponde a `timestamp` SQL Server. CLR <xref:System.TimeSpan?displayProperty=nameWithType> também pode mapear ao SQL Server `TIME` o tipo em alguns casos. O tipo do SQL Server `TIME` foi pretendido representar somente valores positivos menos de 24 horas. CLR <xref:System.TimeSpan> tem um intervalo muito maior.

  > [!NOTE]
  > Os tipos de .NET Framework específicos do SQL Server no <xref:System.Data.SqlTypes> não estão incluídos nessa comparação.

- Incompatíveis no SQL Server:

  - **Tipos de caracteres de comprimento fixo**. O Transact-SQL distingue entre categorias Unicode e não-Unicode e tem três tipos distintos em cada categoria: comprimento fixo `nchar` / `char` , comprimento variável `nvarchar` / `varchar` e tamanho maior `ntext` / `text` . Os tipos de caracteres de comprimento fixo podem ser mapeado para o tipo de CLR <xref:System.Char?displayProperty=nameWithType> para recuperar caracteres, mas não correspondem realmente o mesmo tipo em conversões e comportamento.

  - **Bit**. Embora o domínio de `bit` tem o mesmo número de valores que `Nullable<Boolean>`, os dois tipos são diferentes. `Bit`usa valores `1` e `0` em vez de e `true` / `false` não pode ser usado como um equivalente a expressões boolianas.

  - **Carimbo de data/hora**. Ao contrário do tipo de CLR <xref:System.TimeSpan?displayProperty=nameWithType> , o tipo do SQL Server `TIMESTAMP` representa um número de 8 bytes gerado pelo base de dados que é exclusivo para cada atualização e não é baseado na diferença entre valores de <xref:System.DateTime> .

  - **Money** e **smallmoney**. Esses tipos podem ser mapeados para <xref:System.Decimal> mas são basicamente tipos diferentes e são tratados como esta'n por funções e conversões pelo base.

### <a name="multiple-mappings"></a>Vários mapeamentos

Há muitos tipos de dados do SQL Server que você pode mapear a CLR um ou mais tipos de dados. Também há muitos tipos de CLR que você pode mapear a um ou mais tipos SQL Server. Embora um mapeamento pode ser suportados por LINQ to SQL, não significa que os dois tipos mapeadas entre CLR e o SQL Server são uma correspondência perfeita com precisão, intervalo, e semântica. Alguns mapeamentos podem incluir diferenças em algumas ou todas essas dimensões. Você pode encontrar detalhes sobre essas possíveis diferenças para as várias possibilidades de mapeamento em [mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md).

### <a name="user-defined-types"></a>Tipos definidos pelo usuário

Tipos definidos pelo usuário de CLR são criados para ajudar a ponte entre o intervalo do sistema de tipos. Entretanto problemas surgem interessantes sobre o controle de versão do tipo. Uma alteração na versão do cliente não pode ser correspondida por uma alteração no tipo armazenado no servidor de base de dados. Uma alteração causa um outros tipos incompatíveis onde a semântica de tipo pode não corresponder e o intervalo de versão é provável ficar visível. Uma complicações adicionais ocorrem a hierarquias de herança refactored em sucessivas versões.

## <a name="expression-semantics"></a>Semântica de expressão

Além de por pares a incompatibilidade entre CLR e tipos de base de dados, expressões adicionar complexidade a incompatibilidade. As incompatíveis na semântica de operador, na semântica de função, na conversão implícita de tipos, e as regras de precedência devem ser consideradas.

As seguintes subseções ilustram a incompatibilidade entre expressões aparentemente semelhantes. Talvez seja possível gerar as expressões SQL que são semanticamente equivalentes a uma expressão fornecida de CLR. No entanto, não é claro se semânticas as diferenças entre expressões aparentemente semelhantes são evidentes a um usuário de CLR, e portanto se as alterações que são necessárias para equivalências semântica estão se ou não. Isso é especialmente importante quando um assunto uma expressão é avaliada para um conjunto de valores. A visibilidade da diferença pode depender de dados e ser difícil de identificar durante a codificação e depuração.

### <a name="null-semantics"></a>Semântica nula

As expressões SQL fornecem lógica três avaliada para expressões booleanas. O resultado pode ser true, false, ou zero. Por outro lado, CLR especifica o resultado booleano duas avaliado para as comparações que envolvem valores nulos. Considere o seguinte código:

[!code-csharp[DLinqMismatch#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#2)]
[!code-vb[DLinqMismatch#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#2)]

```sql
-- Assume col1 and col2 are integer columns with null values.
-- Assume that ANSI null behavior has not been explicitly
--  turned off.
Select …
From …
Where col1 = col2
-- Evaluates to null, not true and the corresponding row is not
--   selected.
-- To obtain matching behavior (i -> col1, j -> col2) change
--   the query to the following:
Select …
From …
Where
    col1 = col2
or (col1 is null and col2 is null)
-- (Visual Basic 'Nothing'.)
```

Um problema semelhante ocorre com a suposição sobre resultados duas avaliados.

[!code-csharp[DLinqMismatch#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#3)]
[!code-vb[DLinqMismatch#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#3)]

```sql
-- Assume col1 and col2 are nullable columns.
-- Assume that ANSI null behavior has not been explicitly
--   turned off.
Select …
From …
Where
    col1 = col2
or col1 != col2
-- Visual Basic: col1 <> col2.

-- Excludes the case where the boolean expression evaluates
--   to null. Therefore the where clause does not always
--   evaluate to true.
```

Em casos anteriores, você pode obter o comportamento equivalente em gerar o SQL, mas a conversão não pode exatamente refletir sua intenção.

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não impõe a `null` `nothing` semântica de comparação em C# ou Visual Basic no SQL. Os operadores de comparação são convertidos sintaticamente para seus equivalentes SQL. Semânticas reflete a semântica do SQL como definida pelas configurações do servidor ou de conexão. Dois valores nulos são considerados configurações padrão inferiores desiguais SQL Server (embora você possa alterar as configurações para alterar a semântica). De qualquer forma, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não considera configurações de servidor para a tradução de consulta.

Uma comparação com `null` literal (`nothing`) é convertido para a versão apropriada do SQL (`is null` ou `is not null`).

O valor de `null` (`nothing`) na ordenação é definido pelo SQL Server; [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não altera a ordenação.

### <a name="type-conversion-and-promotion"></a>Conversão de tipos e promoção

O SQL suporta um conjunto rico de conversões implícitas em expressões. As expressões semelhantes em C# exigiriam uma conversão explícita. Por exemplo:

- `Nvarchar` e os tipos de `DateTime` podem ser comparadas em SQL sem nenhuma conversões explícitas; C# requer conversão explícita.

- `Decimal` é convertido implicitamente a `DateTime` no SQL. C# não permite uma conversão implícita.

Também, a precedência de tipo em Transact-SQL difere de precedência de tipo em C# porque o conjunto sendo a base de tipos é diferente. De fato, não há nenhuma relação clara do subconjunto/superconjunto entre as listas de precedência. Por exemplo, `nvarchar` comparar com `varchar` faz com que a conversão implícita da expressão de `varchar` a `nvarchar`. CLR não fornece nenhuma promoção equivalente.

Em casos simples, essas diferenças fazem com que as expressões de CLR com conversões sejam redundantes para uma expressão correspondente SQL. Mais importante, os resultados intermediários de uma expressão SQL podem ser implicitamente promovidos para um tipo que não tem contraparte exata em C#, e vice-versa. Total, os testes, depuração, e a validação dessas expressões adiciona a carga significativa no usuário.

### <a name="collation"></a>Collation

Transact-SQL suporta ordenações explícitas como as anotações a cadeia de caracteres tipo. Essas ordenações determinam a validade de determinadas comparações. Por exemplo, comparar duas colunas com diferentes ordenações explícitas é um erro. O uso do tipo muito mais simples de cadeia de caracteres de CTS não causa esses erros. Considere o seguinte exemplo:

```sql
create table T2 (
    Col1 nvarchar(10),
    Col2      nvarchar(10) collate Latin_general_ci_as
)
```

[!code-csharp[DLinqMismatch#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#4)]
[!code-vb[DLinqMismatch#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#4)]

```sql
Select …
From …
Where Col1 = Col2
-- Error, collation conflict.
```

Na verdade, a subcláusula Collation cria um *tipo restrito* que não é substituível.

Da mesma forma, a ordem de classificação pode ser significativamente diferente entre sistemas de tipos. Essa diferença afeta a classificação dos resultados. <xref:System.Guid> são classificadas em todos os 16 bytes pela ordem lexicographic (`IComparable()`), enquanto T-SQL compara GUIDs na seguinte ordem: (nó 10-15), relógio- segs. (8-9), Hora- alto (6-7), Hora- mid (4-5), Hora- baixo (0-3). Isso regras que foi feito no SQL 7.0 GUIDs gerado quando NT- tinha uma ordem de octeto. A abordagem de assegurou-se que GUIDs gerado no mesmo conjunto de nó viesse juntos em ordem sequencial de acordo com o carimbo de data/hora. A abordagem também é útil para compilar índices (inserções se tornam append em vez de IOs aleatório). A ordem scrambled posteriormente no Windows devido a interesses privacidade, mas o SQL deve manter compatibilidade. Uma solução alternativa é usar <xref:System.Data.SqlTypes.SqlGuid> em vez de <xref:System.Guid> .

### <a name="operator-and-function-differences"></a>Operador e diferenças de função

Os operadores e funções que são essencialmente comparáveis têm a semântica ligeiramente diferente. Por exemplo:

- Especifica C# procura por um caminho menor a semântica com base na ordem lexicalmente de operandos para operadores lógicos `&&` e `||`. O SQL por outro lado é definido para consultas definir - com base e portanto fornece mais liberdade de otimizador para decidir a ordem de execução. Algumas implicações incluem o seguinte:

  - A conversão semanticamente equivalente exigiria " `CASE` ... `WHEN` … `THEN`"constructo no SQL para evitar a reordenação da execução do operando.

  - Uma tradução flexível para `AND` / `OR` operadores poderia causar erros inesperados se a expressão C# depender da avaliação do segundo operando com base no resultado da avaliação do primeiro operando.

- `Round()` a função tem uma semântica diferente no .NET Framework e no T-SQL.

- Iniciar o índice para cadeias de caracteres é 0 em CLR mas 1 no SQL. Portanto, qualquer função que tem a conversão de índice das necessidades de índice.

- O módulo de suporte de CLR (“% ") o operador para números de ponto flutuante mas SQL não.

- O operador de `Like` efetivamente chamando as sobrecargas automático com base em conversões implícitas. Embora o operador de `Like` é definido para operar em tipos de cadeia de caracteres, a conversão implícita de tipos numéricos ou de tipos de `DateTime` permite esses tipos não-cadeia de caracteres a ser usado assim como com `Like` . Em CTS, as conversões implícitas comparáveis não existem. Portanto, as sobrecargas adicionais são necessárias.

    > [!NOTE]
    > Este comportamento do operador de `Like` se aplica a C# somente; a palavra-chave do Visual Basic `Like` é inalterado.

- O estouro sempre é verificado no SQL, mas precisa ser especificado explicitamente em C# (não no Visual Basic) para evitar delimitador. Colunas disponíveis C1, C2 e C3 inteiro, se C1+C2 é armazenado em C3 (atualização T ajustada C3 = C1 + C2).

    ```sql
    create table T3 (
        Col1      integer,
        Col2      integer
    )
    insert into T3 (col1, col2) values (2147483647, 5)
    -- Valid values: max integer value and 5.
    select * from T3 where col1 + col2 < 0
    -- Produces arithmetic overflow error.
    ```

[!code-csharp[DLinqMismatch#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#5)]
[!code-vb[DLinqMismatch#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#5)]

- O SQL executa o arredondamento aritmético simétrico enquanto .NET Framework usa o arredondamento do banco. Consulte o artigo 196652 da knowledgebase para obter detalhes adicionais.

- Por padrão, para localidades comuns, as comparações de cadeia de caracteres não diferenciam maiúsculas de minúsculas no SQL. No Visual Basic e C#, diferenciam maiúsculas de minúsculas. Por exemplo, `s == "Food"` ( `s = "Food"` em Visual Basic) e `s == "Food"` pode produzir resultados diferentes se `s` for `food` .

    ```sql
    -- Assume default US-English locale (case insensitive).
    create table T4 (
        Col1      nvarchar (256)
    )
    insert into T4 values (‘Food’)
    insert into T4 values (‘FOOD’)
    select * from T4 where Col1 = ‘food’
    -- Both the rows are returned because of case-insensitive matching.
    ```

[!code-csharp[DLinqMismatch#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#6)]
[!code-vb[DLinqMismatch#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#6)]

- Funções de operadores aplicadas a fixos argumentos de tipo de caracteres de comprimento em SQL têm a semântica significativamente diferente do que os mesmos operadores/funções aplicados a CLR <xref:System.String?displayProperty=nameWithType>. Isso pode também ser exibido como uma extensão do problema ausente de contrapartes discutido na seção sobre tipos.

    ```sql
    create table T4 (
        Col1      nchar(4)
    )
    Insert into T5(Col1) values ('21');
    Insert into T5(Col1) values ('1021');
    Select * from T5 where Col1 like '%1'
    -- Only the second row with Col1 = '1021' is returned.
    -- Not the first row!
    ```

     [!code-csharp[DLinqMismatch#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#7)]
     [!code-vb[DLinqMismatch#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#7)]

     Um problema semelhante ocorre com concatenação de cadeia de caracteres.

    ```sql
    create table T6 (
        Col1      nchar(4)
        Col2       nchar(4)
    )
    Insert into T6 values ('a', 'b');
    Select Col1+Col2 from T6
    -- Returns concatenation of padded strings "a   b   " and not "ab".
    ```

Em resumo, uma translação complicada pode ser necessária para expressões de CLR e os operadores/funções podem ser necessários para expor a funcionalidade SQL.

### <a name="type-casting"></a>Conversão de tipo

Em C# e no SQL, os usuários podem subtituir a semântica padrão de expressões usando conversões explícitas de tipos (`Cast` e `Convert`). No entanto, expor esse recurso até o limite do sistema de tipos gerencie um dilema. Um SQL converte-se que fornecesse a semântica desejada não pode facilmente ser convertido para uma conversão correspondente C#. Por outro lado, uma conversão C# não pode diretamente ser convertida em um equivalente SQL convertido devido aos tipos incompatíveis, a contrapartes ausente, e para hierarquias diferentes de precedência de tipo. Há uma escolha entre a exposição de incompatibilidade do sistema de tipos e poder significativa perdedora da expressão.

Em outros casos, a conversão de tipo não pode ser necessária em qualquer domínio para validação de uma expressão mas pode ser necessária para certificar-se de que um mapeamento padrão não é aplicado corretamente para a expressão.

```sql
-- Example from "Non-default Mapping" section extended
create table T5 (
    Col1      nvarchar(10),
    Col2      nvarchar(10)
)
Insert into T5(col1, col2) values (‘3’, ‘2’);
```

[!code-csharp[DLinqMismatch#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#8)]
[!code-vb[DLinqMismatch#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#8)]

```sql
Select *
From T5
Where Col1 + Col2 > 4
-- "Col1 + Col2" expr evaluates to '32'
```

## <a name="performance-issues"></a>Problemas de desempenho

A contabilização de algumas diferenças de tipo SQL Server-CLR pode resultar em uma diminuição no desempenho ao cruzar entre os sistemas de tipo CLR e SQL Server. Exemplos de cenários que afetam o desempenho incluem o seguinte:

- Forçado a ordem de classificação para lógico e/ou operadores

- Gerar o SQL para aplicar a ordem de classificação de predicado restringe a capacidade de otimizador SQL.

- Conversões de tipos, se introduzido por um compilador de CLR ou por uma implementação objeto relacional de consulta, podem reduzir o uso de índice.

     Por exemplo,

    ```sql
    -- Table DDL
    create table T5 (
        Col1      varchar(100)
    )
    ```

     [!code-csharp[DLinqMismatch#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#9)]
     [!code-vb[DLinqMismatch#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#9)]

     Considere a conversão de expressão `(s = SOME_STRING_CONSTANT)`.

    ```sql
    -- Corresponding part of SQL where clause
    Where …
    Col1 = SOME_STRING_CONSTANT
    -- This expression is of the form <varchar> = <nvarchar>.
    -- Hence SQL introduces a conversion from varchar to nvarchar,
    --   resulting in
    Where …
    Convert(nvarchar(100), Col1) = SOME_STRING_CONSTANT
    -- Cannot use the index for column Col1 for some implementations.
    ```

Além de diferenças semânticas, é importante considerar impactos o desempenho ao cruzar-se entre o SQL Server e sistemas de tipos de CLR. Para grandes conjuntos de dados, tais problemas de desempenho podem determinar se um aplicativo está deployable.

## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
