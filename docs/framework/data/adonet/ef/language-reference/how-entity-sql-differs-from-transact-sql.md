---
description: 'Saiba mais sobre: como Entity SQL difere do Transact-SQL'
title: Como o Entity SQL difere do Transact-SQL
ms.date: 03/30/2017
ms.assetid: 9c9ee36d-f294-4c8b-a196-f0114c94f559
ms.openlocfilehash: 349dd64cc0e548ab0dc8d0e66e8bb14b58912d09
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696861"
---
# <a name="how-entity-sql-differs-from-transact-sql"></a>Como Entity SQL difere do Transact-SQL

Este artigo descreve as diferenças entre o Entity SQL e o Transact-SQL.  
  
## <a name="inheritance-and-relationships-support"></a>Suporte a herança e relações  

 Entity SQL trabalha diretamente com esquemas de entidade conceitual e dá suporte a recursos de modelo conceitual, como herança e relações.  
  
 Ao trabalhar com herança, geralmente é útil selecionar instâncias de um subtipo de uma coleção de instâncias de supertipo. O operador [OfType](oftype-entity-sql.md) no Entity SQL (semelhante a `oftype` em sequências C#) fornece esse recurso.  
  
## <a name="support-for-collections"></a>Suporte para coleções  

 Entity SQL trata as coleções como entidades de primeira classe. Por exemplo:  
  
- As expressões de coleção são válidas em uma cláusula `from`.  
  
- As subconsultas `in` e `exists` foram generalizadas para permitir quaisquer coleções.  
  
     Um subconsulta é um tipo de coleção. `e1 in e2` e `exists(e)` são as construções de Entity SQL para executar essas operações.  
  
- A operações de conjunto, como `union`, `intersect` e `except`, agora funcionam em coleções.  
  
- As junções funcionam em coleções.  
  
## <a name="support-for-expressions"></a>Suporte para expressões  

 O Transact-SQL tem subconsultas (tabelas) e expressões (linhas e colunas).  
  
 Para dar suporte a coleções e coleções aninhadas, Entity SQL faz tudo uma expressão. Entity SQL é mais combinável do que o Transact-SQL – cada expressão pode ser usada em qualquer lugar. As expressões de consulta sempre resultam em coleções dos tipos projetados e podem ser usadas em qualquer lugar em que uma expressão de coleção seja permitida. Para obter informações sobre expressões Transact-SQL que não têm suporte no Entity SQL, consulte [expressões sem suporte](unsupported-expressions-entity-sql.md).  
  
 A seguir estão todas as consultas de Entity SQL válidas:  
  
```sql  
1+2 *3  
"abc"  
row(1 as a, 2 as b)  
{ 1, 3, 5}
e1 union all e2  
set(e1)  
```  
  
## <a name="uniform-treatment-of-subqueries"></a>Tratamento uniforme de subconsultas  

 Considerando sua ênfase em tabelas, o Transact-SQL executa a interpretação contextual de subconsultas. Por exemplo, uma subconsulta na `from` cláusula é considerada uma multiconjunto (tabela). Mas a mesma subconsulta usada na cláusula `select` é considerada uma subconsulta escalar. Da mesma forma, uma subconsulta usada no lado esquerdo de um `in` operador é considerada uma subconsulta escalar, enquanto o lado direito deve ser uma subconsulta multiconjunto.  
  
 Entity SQL elimina essas diferenças. Uma expressão tem uma interpretação uniforme que não depende do contexto no qual é usada. Entity SQL considera que todas as subconsultas sejam subconsultas multiconjunto. Se um valor escalar for desejado da subconsulta, Entity SQL fornecerá o `anyelement` operador que opera em uma coleção (nesse caso, a subconsulta) e extrairá um valor singleton da coleção.  
  
### <a name="avoiding-implicit-coercions-for-subqueries"></a>Evitando coerções implícitas para subconsultas  

 Um efeito colateral relacionado ao tratamento uniforme de subconsultas é a conversão implícita de subconsultas em valores escalares. Especificamente, no Transact-SQL, um multiconjunto de linhas (com um único campo) é implicitamente convertido em um valor escalar cujo tipo de dados é o do campo.  
  
 Entity SQL não dá suporte a essa coerção implícita. Entity SQL fornece o `ANYELEMENT` operador para extrair um valor singleton de uma coleção e uma `select value` cláusula para evitar a criação de um wrapper de linha durante uma expressão de consulta.  
  
## <a name="select-value-avoiding-the-implicit-row-wrapper"></a>Select Value: evitando o wrapper de linha implícito  

 A cláusula SELECT em uma subconsulta Transact-SQL cria implicitamente um wrapper de linha em volta dos itens na cláusula. Isso indica que não podemos criar coleções de escalares ou objetos. O Transact-SQL permite uma coerção implícita entre um `rowtype` com um campo e um valor singleton do mesmo tipo de dados.  
  
 Entity SQL fornece a `select value` cláusula para ignorar a construção de linha implícita. Somente um item pode ser especificado em uma cláusula `select value`. Quando tal cláusula é usada, nenhum wrapper de linha é construído em volta dos itens na `select` cláusula, e uma coleção da forma desejada pode ser produzida, por exemplo, `select value a` .  
  
 Entity SQL também fornece o Construtor Row para construir linhas arbitrárias. `select` usa um ou mais elementos na projeção e resulta em um registro de dados com campos:  
  
 `select a, b, c`  
  
## <a name="left-correlation-and-aliasing"></a>Correlação à esquerda e aliases  

 No Transact-SQL, as expressões em um determinado escopo (uma única cláusula como `select` ou `from` ) não podem referenciar expressões definidas anteriormente no mesmo escopo. Alguns dialetos do SQL (incluindo Transact-SQL) dão suporte a formas limitadas deles na `from` cláusula.  
  
 Entity SQL generaliza correlações à esquerda na `from` cláusula e as trata uniformemente. As expressões na cláusula `from` podem referenciar as definições anteriores (definições à esquerda) na mesma cláusula sem a necessidade de sintaxe adicional.  
  
 Entity SQL também impõe restrições adicionais em consultas que envolvem `group by` cláusulas. As expressões na `select` cláusula and `having` da cláusula dessas consultas só podem fazer referência às `group by` chaves por meio de seus aliases. A construção a seguir é válida no Transact-SQL, mas não está no Entity SQL:  
  
```sql  
SELECT t.x + t.y FROM T AS t group BY t.x + t.y
```  
  
 Para fazer isso no Entity SQL:  
  
```sql  
SELET k FROM T AS t GROUP BY (t.x + t.y) AS k
```  
  
## <a name="referencing-columns-properties-of-tables-collections"></a>Referenciando colunas (propriedades) de tabelas (coleções)  

 Todas as referências de coluna no Entity SQL devem ser qualificadas com o alias da tabela. A construção a seguir (supondo que `a` seja uma coluna de tabela válida `T` ) é válida no TRANSACT-SQL, mas não no Entity SQL.  
  
```sql  
SELECT a FROM T
```  
  
 O formulário de Entity SQL é  
  
```sql  
SELECT t.a AS A FROM T AS t
```  
  
 Os aliases de tabela são opcionais na cláusula `from`. O nome da tabela é usado como o alias implícito. Entity SQL também permite o seguinte formato:  
  
```sql  
SELET Tab.a FROM Tab
```  
  
## <a name="navigation-through-objects"></a>Navegação por objetos  

 O Transact-SQL usa a notação "." para fazer referência a colunas de (uma linha de) uma tabela. Entity SQL estende essa notação (emprestada de linguagens de programação) para dar suporte à navegação por meio de propriedades de um objeto.  
  
 Por exemplo, se `p` for uma expressão do tipo Person, a seguinte será a sintaxe Entity SQL para referenciar a cidade do endereço dessa pessoa.  
  
```sql  
p.Address.City
```  
  
## <a name="no-support-for-"></a>Não há suporte para \*  

 O Transact-SQL dá suporte à sintaxe não qualificada \* como um alias para toda a linha e a sintaxe qualificada \* (t. \* ) como um atalho para os campos dessa tabela. Além disso, o Transact-SQL permite uma agregação de contagem especial ( \* ), que inclui nulos.  
  
 Entity SQL não dá suporte à construção *. Consultas Transact-SQL do formulário `select * from T` e `select T1.* from T1, T2...` podem ser expressas em Entity SQL como `select value t from T as t` e `select value t1 from T1 as t1, T2 as t2...` , respectivamente. Além disso, essas construções manipulam a herança (substituibilidade do valor), embora as variantes `select *` sejam restritas a propriedades de nível superior do tipo declarado.  
  
 Entity SQL não oferece suporte à `count(*)` agregação. Use `count(0)` em seu lugar.  
  
## <a name="changes-to-group-by"></a>Alterações em group by  

 Entity SQL dá suporte a alias de `group by` chaves. As expressões na `select` cláusula e `having` cláusula devem se referir às `group by` chaves por meio desses aliases. Por exemplo, essa Entity SQL sintaxe:  
  
```sql  
SELECT k1, count(t.a), sum(t.a)
FROM T AS t
GROUP BY t.b + t.c AS k1
```  
  
 ... é equivalente ao Transact-SQL a seguir:  
  
```sql  
SELECT b + c, count(*), sum(a)
FROM T
GROUP BY b + c
```  
  
## <a name="collection-based-aggregates"></a>Agregações baseadas em coleção  

 Entity SQL dá suporte a dois tipos de agregações.  
  
 As agregações baseadas em coleção operam em coleções e geram o resultado agregado. Elas podem aparecer em qualquer lugar na consulta, e não requerem uma cláusula `group by`. Por exemplo:  
  
```sql  
SELECT t.a AS a, count({1,2,3}) AS b FROM T AS t
```  
  
 O Entity SQL também dá suporte a agregações de estilo SQL. Por exemplo:  
  
```sql  
SELECT a, sum(t.b) FROM T AS t GROUP BY t.a AS a
```  
  
## <a name="order-by-clause-usage"></a>Uso da cláusula ORDER BY  

O Transact-SQL permite que as `ORDER BY` cláusulas sejam especificadas somente no bloco de nível superior `SELECT .. FROM .. WHERE` . No Entity SQL, você pode usar uma expressão aninhada `ORDER BY` e ela pode ser colocada em qualquer lugar na consulta, mas a ordenação em uma consulta aninhada não é preservada.  
  
```sql  
-- The following query will order the results by the last name  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact AS C1
        ORDER BY C1.LastName  
```  
  
```sql  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="identifiers"></a>Identificadores  

 No Transact-SQL, a comparação de identificador é baseada no agrupamento do banco de dados atual. No Entity SQL, os identificadores sempre diferenciam maiúsculas de minúsculas e diferenciam acentos (ou seja, Entity SQL diferencia caracteres acentuados e não acentuados; por exemplo, ' a ' não é igual a ' ã '). Entity SQL trata versões de letras que aparecem da mesma forma, mas são de páginas de código diferentes como caracteres diferentes. Para obter mais informações, consulte [conjunto de caracteres de entrada](input-character-set-entity-sql.md).  
  
## <a name="transact-sql-functionality-not-available-in-entity-sql"></a>Funcionalidade Transact-SQL não disponível em Entity SQL  

 A seguinte funcionalidade Transact-SQL não está disponível no Entity SQL.  
  
 DML  
 Atualmente, Entity SQL não fornece suporte para instruções DML (INSERT, Update e Delete).  
  
 DDL  
 O Entity SQL não fornece suporte para DDL na versão atual.  
  
 Programação imperativa  
 O Entity SQL não fornece suporte para programação imperativa, ao contrário do Transact-SQL. Use, em vez disso, uma linguagem de programação.  
  
 Funções de agrupamento  
 Entity SQL ainda não fornece suporte para agrupar funções (por exemplo, CUBE, ROLLUP e GROUPING_SET).  
  
 Funções Analíticas  
 O Entity SQL ainda não fornece suporte para funções analíticas.  
  
 Funções internas, operadores  
 O Entity SQL dá suporte a um subconjunto de funções e operadores internos do Transact-SQL. Esses operadores e funções provavelmente têm suporte com os principais provedores de repositório. Entity SQL usa funções específicas do repositório declaradas em um manifesto do provedor. Além disso, o Entity Framework permite que você declare funções de armazenamento existentes internas e definidas pelo usuário, para Entity SQL usar.  
  
 Dicas  
 Entity SQL não fornece mecanismos para dicas de consulta.  
  
 Processando resultados de consulta em lotes  
 Entity SQL não dá suporte a resultados de consulta em lote. Por exemplo, o seguinte é um Transact-SQL válido (envio como um lote):  
  
```sql  
SELECT * FROM products;
SELECT * FROM catagories;
```  
  
 No entanto, não há suporte para o Entity SQL equivalente:  
  
```sql  
SELECT value p FROM Products AS p;
SELECT value c FROM Categories AS c;
```  
  
 Entity SQL só dá suporte a uma instrução de consulta de produção de resultado por comando.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da Entity SQL](entity-sql-overview.md)
- [Expressões sem suporte](unsupported-expressions-entity-sql.md)
