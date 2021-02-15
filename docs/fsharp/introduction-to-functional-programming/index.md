---
title: Introdução à programação funcional em F#
description: 'Aprenda os conceitos básicos da programação funcional em F #.'
ms.date: 10/29/2018
ms.openlocfilehash: 44242a4319a331312a003a555d1483f2a3f1a90d
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110579"
---
# <a name="introduction-to-functional-programming-in-f"></a>Introdução à programação funcional em F\#

A programação funcional é um estilo de programação que enfatiza o uso de funções e dados imutáveis. A programação funcional digitada é quando a programação funcional é combinada com tipos estáticos, como com F #. Em geral, os seguintes conceitos são enfatizados na programação funcional:

* Funções como as construções primárias que você usa
* Expressões em vez de instruções
* Valores imutáveis sobre variáveis
* Programação declarativa sobre programação imperativa

Em toda esta série, você explorará os conceitos e padrões na programação funcional usando F #. Ao longo do caminho, você aprenderá também com o F #.

## <a name="terminology"></a>Terminologia

A programação funcional, como outros paradigmas de programação, vem com um vocabulário que você eventualmente precisará aprender. Aqui estão alguns termos comuns que você verá todo o tempo:

* **Função** – uma função é uma construção que produzirá uma saída quando uma entrada for fornecida. Mais formalmente, ele _mapeia_ um item de um conjunto para outro definido. Essa formalização é levantada no concreto de várias maneiras, especialmente ao usar funções que operam em coleções de dados. É o conceito mais básico (e importante) na programação funcional.
* **Expressão** -uma expressão é um constructo no código que produz um valor. Em F #, esse valor deve ser associado ou ignorado explicitamente. Uma expressão pode ser substituída trivial por uma chamada de função.
* **Pureza** -pureza é uma propriedade de uma função, de modo que seu valor de retorno é sempre o mesmo para os mesmos argumentos e que sua avaliação não tem efeitos colaterais. Uma função pura depende inteiramente de seus argumentos.
* **Transparência referencial** -transparência referencial é uma propriedade de expressões, de modo que elas possam ser substituídas por sua saída sem afetar o comportamento de um programa.
* **Imutabilidade** -imutabilidade significa que um valor não pode ser alterado in-loco. Isso está em contraste com variáveis, que podem ser alteradas no local.

## <a name="examples"></a>Exemplos

Os exemplos a seguir demonstram esses conceitos principais.

### <a name="functions"></a>Funções

A construção mais comum e fundamental na programação funcional é a função. Aqui está uma função simples que adiciona 1 a um inteiro:

```fsharp
let addOne x = x + 1
```

Sua assinatura de tipo é a seguinte:

```fsharp
val addOne: x:int -> int
```

A assinatura pode ser lida como " `addOne` aceita um `int` nome `x` e produzirá um `int` ". Mais formalmente, `addOne` está _mapeando_ um valor do conjunto de inteiros para o conjunto de inteiros. O `->` token significa esse mapeamento. Em F #, normalmente você pode examinar a assinatura da função para ter um sentido para o que ela faz.

Então, por que a assinatura é importante? Na programação funcional digitada, a implementação de uma função é geralmente menos importante do que a assinatura de tipo real! O fato de `addOne` Adicionar o valor 1 a um inteiro é interessante em tempo de execução, mas quando você está construindo um programa, o fato de ele aceitar e retorna um `int` é o que informa como você realmente usará essa função. Além disso, depois de usar essa função corretamente (com relação à sua assinatura de tipo), o diagnóstico de qualquer problema pode ser feito somente dentro do corpo da `addOne` função. Este é o ímpeto por trás da programação funcional de tipo.

### <a name="expressions"></a>Expressões

As expressões são construções que são avaliadas como um valor. Em contraste com as instruções, que executam uma ação, as expressões podem ser consideradas para executar uma ação que retorna um valor. As expressões são quase sempre usadas em programação funcional em vez de instruções.

Considere a função anterior, `addOne` . O corpo de `addOne` é uma expressão:

```fsharp
// 'x + 1' is an expression!
let addOne x = x + 1
```

É o resultado dessa expressão que define o tipo de resultado da `addOne` função. Por exemplo, a expressão que compõe essa função pode ser alterada para ser um tipo diferente, como `string` :

```fsharp
let addOne x = x.ToString() + "1"
```

A assinatura da função agora é:

```fsharp
val addOne: x:'a -> string
```

Como qualquer tipo em F # pode ter `ToString()` sido chamado, o tipo de foi `x` tornado genérico (chamado de [generalização automática](../language-reference/generics/automatic-generalization.md)) e o tipo resultante é um `string` .

As expressões não são apenas os corpos de funções. Você pode ter expressões que produzem um valor que você usa em outro lugar. Um comum é `if` :

```fsharp
// Checks if 'x' is odd by using the mod operator
let isOdd x = x % 2 <> 0

let addOneIfOdd input =
    let result =
        if isOdd input then
            input + 1
        else
            input

    result
```

A `if` expressão produz um valor chamado `result` . Observe que você poderia omitir `result` inteiramente, tornando a `if` expressão o corpo da `addOneIfOdd` função. O importante a ser lembrado sobre expressões é que elas produzem um valor.

Há um tipo especial, `unit` , que é usado quando não há nada para retornar. Por exemplo, considere esta simples função:

```fsharp
let printString (str: string) =
    printfn $"String is: {str}"
```

A assinatura é parecida com esta:

```fsharp
val printString: str:string -> unit
```

O `unit` tipo indica que não há nenhum valor real sendo retornado. Isso é útil quando você tem uma rotina que deve "fazer trabalho", apesar de não ter nenhum valor para retornar como resultado desse trabalho.

Isso é um contraste nítido à programação imperativa, em que a `if` construção equivalente é uma instrução, e a produção de valores geralmente é feita com variáveis de mutação. Por exemplo, em C#, o código pode ser escrito da seguinte maneira:

```csharp
bool IsOdd(int x) => x % 2 != 0;

int AddOneIfOdd(int input)
{
    var result = input;

    if (IsOdd(input))
    {
        result = input + 1;
    }

    return result;
}
```

Vale a pena observar que o C# e outras linguagens de estilo C oferecem suporte à [expressão Ternário](../../csharp/language-reference/operators/conditional-operator.md), que permite a programação condicional baseada em expressão.

Na programação funcional, é raro converter valores com instruções. Embora algumas linguagens funcionais suportem instruções e mutação, não é comum usar esses conceitos na programação funcional.

### <a name="pure-functions"></a>Funções puras

Como mencionado anteriormente, as funções puras são funções que:

* Sempre avalie o mesmo valor para a mesma entrada.
* Não têm efeitos colaterais.

É útil considerar as funções matemáticas neste contexto. Na matemática, as funções dependem apenas de seus argumentos e não têm nenhum efeito colateral. Na função matemática `f(x) = x + 1` , o valor de `f(x)` depende apenas do valor de `x` . Funções puras na programação funcional são as mesmas.

Ao escrever uma função pura, a função deve depender apenas de seus argumentos e não executar nenhuma ação que resulte em um efeito colateral.

Aqui está um exemplo de uma função não pura porque depende do estado global e mutável:

```fsharp
let mutable value = 1

let addOneToValue x = x + value
```

A `addOneToValue` função é claramente impura, pois `value` pode ser alterada a qualquer momento para ter um valor diferente de 1. Esse padrão de dependendo de um valor global é ser evitado na programação funcional.

Aqui está outro exemplo de uma função não pura, pois ela executa um efeito colateral:

```fsharp
let addOneToValue x =
    printfn $"x is %d{x}"
    x + 1
```

Embora essa função não dependa de um valor global, ela grava o valor de na `x` saída do programa. Embora não haja nada inerentemente errado com isso, isso significa que a função não é pura. Se outra parte do seu programa depender de algo externo ao programa, como o buffer de saída, chamar essa função poderá afetar a outra parte do programa.

A remoção da `printfn` instrução torna a função pura:

```fsharp
let addOneToValue x = x + 1
```

Embora essa função não seja inerentemente _melhor_ do que a versão anterior com a `printfn` instrução, ela garante que toda essa função seja retornar um valor. Chamar essa função quantas vezes produz o mesmo resultado: ele apenas produz um valor. A previsibilidade fornecida pela pureza é algo que muitos programadores funcionais buscam.

### <a name="immutability"></a>Imutabilidade

Finalmente, um dos conceitos mais fundamentais da programação funcional tipada é a imutabilidade. Em F #, todos os valores são imutáveis por padrão. Isso significa que eles não podem ser modificados in-loco, a menos que você os marque explicitamente como mutável.

Na prática, trabalhar com valores imutáveis significa que você altera sua abordagem de programação de, "preciso alterar algo", para "preciso produzir um novo valor".

Por exemplo, adicionar 1 a um valor significa produzir um novo valor, não mutando o existente:

```fsharp
let value = 1
let secondValue = value + 1
```

Em F #, o código a seguir **não modifica a** `value` função; em vez disso, ele executa uma verificação de igualdade:

```fsharp
let value = 1
value = value + 1 // Produces a 'bool' value!
```

Algumas linguagens de programação funcional não oferecem suporte a mutação. Em F #, ele tem suporte, mas não é o comportamento padrão para valores.

Esse conceito se estende ainda mais às estruturas de dados. Na programação funcional, estruturas de dados imutáveis como conjuntos (e muito mais) têm uma implementação diferente da que você pode esperar inicialmente. Conceitualmente, algo como adicionar um item a um conjunto não altera o conjunto, ele produz um _novo_ conjunto com o valor adicionado. Nos bastidores, isso geralmente é feito por uma estrutura de dados diferente que permite controlar com eficiência um valor para que a representação apropriada dos dados possa ser fornecida como resultado.

Esse estilo de trabalho com valores e estruturas de dados é essencial, pois ele o força a tratar qualquer operação que modifique algo como se ele criasse uma nova versão dessa coisa. Isso permite que coisas como igualdade e comparação sejam consistentes em seus programas.

## <a name="next-steps"></a>Próximas etapas

A próxima seção abordará minuciosamente as funções, explorando diferentes maneiras de usá-las na programação funcional.

As [funções de primeira classe](first-class-functions.md) exploram as funções profundamente, mostrando como você pode usá-las em vários contextos.

## <a name="further-reading"></a>Leitura adicional

A série de [funções de raciocínio](https://fsharpforfunandprofit.com/posts/thinking-functionally-intro/) é outro excelente recurso para aprender sobre a programação funcional com F #. Ele aborda os conceitos básicos da programação funcional de forma pragmática e fácil de ler, usando recursos F # para ilustrar os conceitos.
