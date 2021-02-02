---
title: Criando tipos (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 41fa7bde-8d20-4a3f-a3d2-fb791e128010
ms.openlocfilehash: 89b4c3bb8b9d69767aa30cee5331269537c084bd
ms.sourcegitcommit: 38999dc0ec4f7c4404de5ce0951b64c55997d9ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99427017"
---
# <a name="constructing-types-entity-sql"></a>Criando tipos (Entity SQL)

<!-- markdownlint-disable DOCSMD001 -->
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornece três tipos de construtores: construtores de linha, construtores de tipo nomeado e construtores de coleção.

## <a name="row-constructors"></a>Coloque construtores

Você usa construtores de linha em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] para construir registros anônimos, tipados estrutural de um ou mais valores. O tipo do resultado de um construtor de linha é um tipo de linha cujos tipos de campo correspondem aos tipos de valores usados para construir a linha. Por exemplo, a expressão a seguir constrói um valor do tipo `Record(a int, b string, c int)` :

`ROW(1 AS a, "abc" AS b, a + 34 AS c)`

Se você não fornecer um alias para um construtor de expressão em seguida, Entity Framework tentará gerar um. Para obter mais informações, consulte a seção "regras de alias" em [identificadores](identifiers-entity-sql.md).

As seguintes regras se aplicam para o construtor de serrilha de expressão em uma linha:

- O construtor das expressões em uma linha não pode referenciar outras alias no mesmo construtor.
- Duas expressões no mesmo construtor de linha não podem ter as mesmas alias.

Para obter mais informações sobre construtores de linha, consulte [Row](row-entity-sql.md).

## <a name="collection-constructors"></a>Construtores de coleção

Você usa construtores de coleção em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] para criar uma instância de um multiset de uma lista de valores. Todos os valores no construtor deve ser do tipo correspondente mutuamente `T`, e o construtor gerenciar uma coleção do tipo `Multiset<T>`. Por exemplo, a expressão a seguir cria uma coleção de inteiros:

`Multiset(1, 2, 3)`

`{1, 2, 3}`

Não são permitidos construtores vazios de multiset porque o tipo dos elementos não pode ser determinado. O seguinte é válido:

`multiset() {}`

Para obter mais informações, consulte [MultiSet](multiset-entity-sql.md).

## <a name="named-type-constructors-namedtype-initializers"></a>Construtores nomes de tipo (inicializadores de NamedType)

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] permite que os construtores de tipo (inicializadores) criar instâncias de tipos complexos nomeados e tipos de entidade. Por exemplo, a expressão a seguir cria uma instância de um tipo de `Person` .

`Person("abc", 12)`

A expressão a seguir cria uma instância de um tipo complexo.

`MyModel.ZipCode(‘98118’, ‘4567’)`

A expressão a seguir cria uma instância de um tipo complexo aninhado.

`MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`

A expressão a seguir cria uma instância de um objeto com um tipo complexo aninhado.

`MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`

O exemplo a seguir mostra como inicializar uma propriedade de um tipo complexo para nulo. `MyModel.ZipCode(‘98118’, null)`

Os argumentos para o construtor são considerados para estar na mesma ordem que a declaração de atributos de tipo.

Para obter mais informações, consulte [Construtor de tipo nomeado](named-type-constructor-entity-sql.md).

## <a name="see-also"></a>Confira também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Visão geral da Entity SQL](entity-sql-overview.md)
- [Sistema de tipo](type-system-entity-sql.md)
