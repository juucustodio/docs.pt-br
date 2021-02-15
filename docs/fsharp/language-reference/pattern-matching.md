---
title: Correspondência padrão
description: 'Saiba como os padrões são usados em F # para comparar dados com estruturas lógicas, decompor dados em partes constituintes ou extrair informações de dados.'
ms.date: 11/12/2020
ms.openlocfilehash: 932f50b7947f6df728149437dd3ceb19c42e5c6a
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740270"
---
# <a name="pattern-matching"></a>Correspondência padrão

Padrões são regras para transformar dados de entrada. Eles são usados em toda a linguagem F # para comparar dados com uma estrutura lógica ou estruturas, decompor dados em partes constituintes ou extrair informações de dados de várias maneiras.

## <a name="remarks"></a>Comentários

Padrões são usados em muitas construções de linguagem, como a `match` expressão. Eles são usados quando você está processando argumentos para funções em `let` associações, expressões lambda e nos manipuladores de exceção associados à `try...with` expressão. Para obter mais informações, consulte [corresponder expressões](match-expressions.md), [permitir associações](./functions/let-bindings.md), [expressões lambda: a `fun` palavra-chave](./functions/lambda-expressions-the-fun-keyword.md)e [exceções: a `try...with` expressão](./exception-handling/the-try-with-expression.md).

Por exemplo, na `match` expressão, o *padrão* é o que segue o símbolo de pipe.

```fsharp
match expression with
| pattern [ when condition ] -> result-expression
...
```

Cada padrão atua como uma regra para transformar a entrada de alguma maneira. Na `match` expressão, cada padrão é examinado, por sua vez, para ver se os dados de entrada são compatíveis com o padrão. Se uma correspondência for encontrada, a expressão de resultado será executada. Se uma correspondência não for encontrada, a próxima regra de padrão será testada. A parte de *condição* opcional quando é explicada em [expressões de correspondência](match-expressions.md).

Os padrões com suporte são mostrados na tabela a seguir. Em tempo de execução, a entrada é testada em relação a cada um dos seguintes padrões na ordem listada na tabela, e os padrões são aplicados recursivamente, de primeiro até o último, conforme aparecem no seu código e da esquerda para a direita para os padrões em cada linha.

|Nome|Descrição|Exemplo|
|----|-----------|-------|
|Padrão de constante|Qualquer literal numérico, de caractere ou de cadeia de caracteres, uma constante de enumeração ou um identificador literal definido|`1.0`, `"test"`, `30`, `Color.Red`|
|Padrão de identificador|Um valor de case de uma união discriminada, um rótulo de exceção ou um caso de padrão ativo|`Some(x)`<br /><br />`Failure(msg)`|
|Padrão de variável|*identifier*|`a`|
|`as` padrão|*padrão* como *identificador*|`(a, b) as tuple1`|
|OU padrão|*pattern1* &#124; *pattern2*|<code>([h] &#124; [h; _])</code>|
|E padrão|*pattern1* &amp; *pattern2*|`(a, b) & (_, "test")`|
|Padrão de contras|*identificador* :: *lista-identificador*|`h :: t`|
|Padrão de lista|[ *pattern_1*;...; *pattern_n* ]|`[ a; b; c ]`|
|Padrão de matriz|[&#124; *pattern_1*;..; *pattern_n* &#124;]|<code>[&#124; a; b; c &#124;]</code>|
|Padrão entre parênteses|( *padrão* )|`( a )`|
|Padrão de tupla|( *pattern_1*,..., *pattern_n* )|`( a, b )`|
|Padrão de registro|{ *identifier1*  =  *pattern_1*; ... ; *identifier_n*  =  *pattern_n* }|`{ Name = name; }`|
|Padrão de curinga|_|`_`|
|Padrão junto com a anotação de tipo|*padrão* : *tipo*|`a : int`|
|Padrão de teste de tipo|:? *tipo* [como *identificador* ]|`:? System.DateTime as dt`|
|Padrão nulo|null|`null`|
|Padrão nameof|*expr nameof*|`nameof str`|

## <a name="constant-patterns"></a>Padrões constantes

Os padrões constantes são numéricos, caracteres e literais de cadeia de caracteres, constantes de enumeração (com o nome do tipo de enumeração incluído). Uma `match` expressão que tem apenas padrões constantes pode ser comparada a uma instrução Case em outras linguagens. A entrada é comparada com o valor literal e o padrão corresponde se os valores são iguais. O tipo do literal deve ser compatível com o tipo de entrada.

O exemplo a seguir demonstra o uso de padrões literais e também usa um padrão variável e um padrão ou.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4801.fs)]

Outro exemplo de um padrão literal é um padrão baseado em constantes de enumeração. Você deve especificar o nome do tipo de enumeração ao usar constantes de enumeração.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4802.fs)]

## <a name="identifier-patterns"></a>Padrões de identificador

Se o padrão for uma cadeia de caracteres que forma um identificador válido, a forma do identificador determinará como o padrão é correspondido. Se o identificador for maior que um único caractere e começar com um caractere maiúsculo, o compilador tentará fazer uma correspondência com o padrão de identificador. O identificador desse padrão pode ser um valor marcado com o atributo literal, um caso união discriminado, um identificador de exceção ou um caso de padrão ativo. Se nenhum identificador correspondente for encontrado, a correspondência falhará e a próxima regra de padrão, o padrão variável, será comparada com a entrada.

Os padrões de União discriminados podem ser casos nomeados simples ou podem ter um valor, ou uma tupla contendo vários valores. Se houver um valor, você deverá especificar um identificador para o valor. No caso de uma tupla, você deve fornecer um padrão de tupla com um identificador para cada elemento da tupla ou um identificador com um nome de campo para um ou mais campos de União nomeados. Consulte os exemplos de código nesta seção para obter exemplos.

O `option` tipo é uma união discriminada que tem dois casos `Some` e `None` . Um case ( `Some` ) tem um valor, mas o outro ( `None` ) é apenas um caso nomeado. Portanto, `Some` o precisa ter uma variável para o valor associado ao `Some` caso, mas `None` deve aparecer por si só. No código a seguir, a variável `var1` recebe o valor obtido pela correspondência ao `Some` caso.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4803.fs)]

No exemplo a seguir, a `PersonName` união discriminada contém uma mistura de cadeias e caracteres que representam possíveis formas de nomes. Os casos da união discriminada são `FirstOnly` , `LastOnly` e `FirstLast` .

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4804.fs)]

Para uniões discriminadas que têm campos nomeados, use o sinal de igual (=) para extrair o valor de um campo nomeado. Por exemplo, considere uma união discriminada com uma declaração como a seguinte.

```fsharp
type Shape =
    | Rectangle of height : float * width : float
    | Circle of radius : float
```

Você pode usar os campos nomeados em uma expressão de correspondência de padrões da seguinte maneira.

```fsharp
let matchShape shape =
    match shape with
    | Rectangle(height = h) -> printfn $"Rectangle with length %f{h}"
    | Circle(r) -> printfn $"Circle with radius %f{r}"
```

O uso do campo nomeado é opcional, portanto, no exemplo anterior, ambos `Circle(r)` e `Circle(radius = r)` têm o mesmo efeito.

Quando você especifica vários campos, use o ponto-e-vírgula (;) como um separador.

```fsharp
match shape with
| Rectangle(height = h; width = w) -> printfn $"Rectangle with height %f{h} and width %f{w}"
| _ -> ()
```

Os padrões ativos permitem definir correspondência de padrões personalizados mais complexos. Para obter mais informações sobre padrões ativos, consulte [padrões ativos](active-patterns.md).

O caso em que o identificador é uma exceção é usado na correspondência de padrões no contexto de manipuladores de exceção. Para obter informações sobre correspondência de padrões no tratamento de exceção, consulte [Exceptions: The `try...with` expression](./exception-handling/the-try-with-expression.md).

## <a name="variable-patterns"></a>Padrões de variáveis

O padrão variável atribui o valor que está sendo correspondido a um nome de variável, que está disponível para uso na expressão de execução à direita do `->` símbolo. Um padrão variável sozinho corresponde A qualquer entrada, mas padrões de variáveis geralmente aparecem dentro de outros padrões, permitindo, portanto, estruturas mais complexas, como tuplas e matrizes a serem decompostas em variáveis.

O exemplo a seguir demonstra um padrão variável dentro de um padrão de tupla.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4805.fs)]

## <a name="as-pattern"></a>como padrão

O `as` padrão é um padrão que tem uma `as` cláusula acrescentada a ele. A `as` cláusula associa o valor correspondente a um nome que pode ser usado na expressão de execução de uma `match` expressão ou, no caso em que esse padrão é usado em uma `let` associação, o nome é adicionado como uma associação ao escopo local.

O exemplo a seguir usa um `as` padrão.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4806.fs)]

## <a name="or-pattern"></a>OU padrão

O padrão ou é usado quando os dados de entrada podem corresponder a vários padrões e você deseja executar o mesmo código como resultado. Os tipos de ambos os lados do padrão ou devem ser compatíveis.

O exemplo a seguir demonstra o padrão ou.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4807.fs)]

## <a name="and-pattern"></a>E padrão

O padrão AND requer que a entrada corresponda a dois padrões. Os tipos de ambos os lados do padrão e devem ser compatíveis.

O exemplo a seguir é como `detectZeroTuple` mostrado na seção padrão de tupla mais adiante neste tópico, mas aqui `var1` e `var2` são obtidos como valores usando o padrão e.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4808.fs)]

## <a name="cons-pattern"></a>Padrão de contras

O padrão de contras de contras é usado para decompor uma lista no primeiro elemento, no *cabeçalho* e em uma lista que contém os elementos restantes, a *parte final*.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4809.fs)]

## <a name="list-pattern"></a>Padrão de lista

O padrão de lista permite que as listas sejam decompostas em vários elementos. O próprio padrão de lista pode corresponder apenas a listas de um número específico de elementos.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4810.fs)]

## <a name="array-pattern"></a>Padrão de matriz

O padrão de matriz é semelhante ao padrão de lista e pode ser usado para decompor matrizes de um comprimento específico.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4811.fs)]

## <a name="parenthesized-pattern"></a>Padrão entre parênteses

Os parênteses podem ser agrupados de acordo com os padrões para alcançar a associação desejada. No exemplo a seguir, os parênteses são usados para controlar a associação entre um padrão e um padrão de contras.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4812.fs)]

## <a name="tuple-pattern"></a>Padrão de tupla

O padrão de tupla corresponde à entrada no formulário de tupla e permite que a tupla seja decomposta em seus elementos constituintes usando variáveis de correspondência de padrões para cada posição na tupla.

O exemplo a seguir demonstra o padrão de tupla e também usa padrões literais, padrões variáveis e o padrão curinga.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4813.fs)]

## <a name="record-pattern"></a>Padrão de registro

O padrão de registro é usado para decompor registros para extrair os valores dos campos. O padrão não precisa fazer referência a todos os campos do registro; os campos omitidos simplesmente não participam da correspondência e não são extraídos.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4814.fs)]

## <a name="wildcard-pattern"></a>Padrão de curinga

O padrão de caractere curinga é representado pelo caractere de sublinhado ( `_` ) e corresponde a qualquer entrada, assim como o padrão de variável, exceto que a entrada é descartada em vez de atribuída a uma variável. O padrão de caractere curinga geralmente é usado em outros padrões como um espaço reservado para valores que não são necessários na expressão à direita do `->` símbolo. O padrão curinga também é usado frequentemente no final de uma lista de padrões para corresponder a qualquer entrada sem correspondência. O padrão de curinga é demonstrado em muitos exemplos de código neste tópico. Consulte o código anterior para obter um exemplo.

## <a name="patterns-that-have-type-annotations"></a>Padrões que têm anotações de tipo

Os padrões podem ter anotações de tipo. Eles se comportam como outras anotações de tipo e inferência de guia como outras anotações de tipo. Os parênteses são necessários em relação a anotações de tipo em padrões. O código a seguir mostra um padrão que tem uma anotação de tipo.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4815.fs)]

## <a name="type-test-pattern"></a>Padrão de teste de tipo

O padrão de teste de tipo é usado para corresponder à entrada em relação a um tipo. Se o tipo de entrada for uma correspondência (ou um tipo derivado) do tipo especificado no padrão, a correspondência será realizada com sucesso.

O exemplo a seguir demonstra o tipo de padrão de teste.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4816.fs)]

Se você estiver verificando apenas se um identificador é de um tipo derivado específico, não precisará da `as identifier` parte do padrão, conforme mostrado no exemplo a seguir:

```fsharp
type A() = class end
type B() = inherit A()
type C() = inherit A()

let m (a: A) =
    match a with
    | :? B -> printfn "It's a B"
    | :? C -> printfn "It's a C"
    | _ -> ()
```

## <a name="null-pattern"></a>Padrão nulo

O padrão nulo corresponde ao valor nulo que pode aparecer quando você está trabalhando com tipos que permitem um valor nulo. Padrões nulos são usados frequentemente quando interoperam com código .NET Framework. Por exemplo, o valor de retorno de uma API do .NET pode ser a entrada para uma `match` expressão. Você pode controlar o fluxo do programa com base em se o valor de retorno é nulo e também em outras características do valor retornado. Você pode usar o padrão nulo para impedir que valores nulos se propaguem para o restante do seu programa.

O exemplo a seguir usa o padrão nulo e o padrão de variável.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4817.fs)]

## <a name="nameof-pattern"></a>Padrão nameof

O `nameof` padrão corresponde a uma cadeia de caracteres quando seu valor é igual à expressão que segue a `nameof` palavra-chave. Por exemplo:

```fsharp
let f (str: string) =
    match str with
    | nameof str -> "It's 'str'!"
    | _ -> "It is not 'str'!"

f "str" // matches
f "asdf" // does not match
```

Consulte o [`nameof`](nameof.md) operador para obter informações sobre o que você pode obter um nome.

## <a name="see-also"></a>Confira também

- [Expressões de correspondência](match-expressions.md)
- [Padrões ativos](active-patterns.md)
- [Referência de linguagem F #](index.md)
