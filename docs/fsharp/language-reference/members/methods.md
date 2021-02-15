---
title: Métodos
description: 'Saiba como um método F # é uma função associada a um tipo que é usado para expor e implementar a funcionalidade e o comportamento de objetos e tipos.'
ms.date: 11/04/2019
ms.openlocfilehash: 6f5ae76ea450b07763eb58d0c95b18b30f634551
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224107"
---
# <a name="methods"></a>Métodos

Um *método* é uma função associada a um tipo. Na programação orientada a objeto, os métodos são usados para expor e implementar a funcionalidade e o comportamento de objetos e tipos.

## <a name="syntax"></a>Sintaxe

```fsharp
// Instance method definition.
[ attributes ]
member [inline] self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Static method definition.
[ attributes ]
static member [inline] method-name parameter-list [ : return-type ] =
    method-body

// Abstract method declaration or virtual dispatch slot.
[ attributes ]
abstract member method-name : type-signature

// Virtual method declaration and default implementation.
[ attributes ]
abstract member method-name : type-signature
[ attributes ]
default self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Override of inherited virtual method.
[ attributes ]
override self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Optional and DefaultParameterValue attributes on input parameters
[ attributes ]
[ modifier ] member [inline] self-identifier.method-name ([<Optional; DefaultParameterValue( default-value )>] input) [ : return-type ]
```

## <a name="remarks"></a>Comentários

Na sintaxe anterior, você pode ver as várias formas de declarações e definições de método. Em corpos de métodos mais longos, uma quebra de linha segue o sinal de igual (=) e o corpo do método inteiro é recuado.

Atributos podem ser aplicados a qualquer declaração de método. Elas precedem a sintaxe para uma definição de método e geralmente são listadas em uma linha separada. Para obter mais informações, consulte [Atributos](../attributes.md).

Os métodos podem ser marcados `inline` . Para saber mais sobre `inline`, veja [Funções embutidas](../functions/inline-functions.md).

Métodos não embutidos podem ser usados recursivamente dentro do tipo; Não é necessário usar a `rec` palavra-chave explicitamente.

## <a name="instance-methods"></a>Métodos de instância

Os métodos de instância são declarados com a `member` palavra-chave e um *autoidentificador*, seguidos por um ponto (.) e o nome do método e os parâmetros. Como é o caso de `let` associações, a *lista de parâmetros* pode ser um padrão. Normalmente, você coloca parâmetros de método entre parênteses em um formulário de tupla, que é a maneira como os métodos aparecem em F # quando eles são criados em outros idiomas de .NET Framework. No entanto, o formulário na forma curried (parâmetros separados por espaços) também é comum e também há suporte para outros padrões.

O exemplo a seguir ilustra a definição e o uso de um método de instância não abstrata.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3401.fs)]

Em métodos de instância, não use o autoidentifier para acessar os campos definidos usando Let bindings. Use o autoidentifier ao acessar outros membros e propriedades.

## <a name="static-methods"></a>Métodos estáticos

A palavra-chave `static` é usada para especificar que um método pode ser chamado sem uma instância e não está associado a uma instância de objeto. Caso contrário, os métodos são métodos de instância.

O exemplo na próxima seção mostra os campos declarados com a `let` palavra-chave, os membros da propriedade declarados com a `member` palavra-chave e um método estático declarado com a `static` palavra-chave.

O exemplo a seguir ilustra a definição e o uso de métodos estáticos. Suponha que essas definições de método estejam na `SomeType` classe da seção anterior.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3402.fs)]

## <a name="abstract-and-virtual-methods"></a>Métodos abstratos e virtuais

A palavra-chave `abstract` indica que um método tem um slot de expedição virtual e pode não ter uma definição na classe. Um *slot de expedição virtual* é uma entrada em uma tabela mantida internamente de funções que é usada em tempo de execução para pesquisar chamadas de função virtual em um tipo orientado a objeto. O mecanismo de expedição virtual é o mecanismo que implementa o *polimorfismo*, um recurso importante da programação orientada a objeto. Uma classe que tem pelo menos um método abstrato sem uma definição é uma *classe abstrata*, o que significa que nenhuma instância pode ser criada dessa classe. Para obter mais informações sobre classes abstratas, consulte [classes abstratas](../abstract-classes.md).

Declarações de método abstract não incluem um corpo de método. Em vez disso, o nome do método é seguido por dois-pontos (:) e uma assinatura de tipo para o método. A assinatura de tipo de um método é igual à mostrada pelo IntelliSense quando você pausa o ponteiro do mouse sobre um nome de método no editor de Visual Studio Code, exceto sem nomes de parâmetros. As assinaturas de tipo também são exibidas pelo intérprete, fsi.exe, quando você estiver trabalhando interativamente. A assinatura de tipo de um método é formada pela listagem dos tipos dos parâmetros, seguidos pelo tipo de retorno, com os símbolos de separadores apropriados. Os parâmetros na forma curried são separados por `->` e os parâmetros de tupla são separados por `*` . O valor de retorno é sempre separado dos argumentos por um `->` símbolo. Os parênteses podem ser usados para agrupar parâmetros complexos, como quando um tipo de função é um parâmetro ou para indicar quando uma tupla é tratada como um único parâmetro, e não como dois parâmetros.

Você também pode fornecer definições padrão de métodos abstratos adicionando a definição à classe e usando a `default` palavra-chave, conforme mostrado no bloco de sintaxe neste tópico. Um método abstrato que tem uma definição na mesma classe é equivalente a um método virtual em outras linguagens de .NET Framework. Se houver ou não uma definição, a `abstract` palavra-chave criará um novo slot de expedição na tabela de funções virtuais para a classe.

Independentemente de uma classe base implementar seus métodos abstratos, as classes derivadas podem fornecer implementações de métodos abstratos. Para implementar um método abstract em uma classe derivada, defina um método que tenha o mesmo nome e assinatura na classe derivada, exceto use a `override` `default` palavra-chave ou e forneça o corpo do método. As palavras-chave `override` e `default` significam exatamente a mesma coisa. Use `override` se o novo método substituir uma implementação de classe base; use `default` quando você criar uma implementação na mesma classe que a declaração abstrata original. Não use a `abstract` palavra-chave no método que implementa o método que foi declarado abstrato na classe base.

O exemplo a seguir ilustra um método abstrato `Rotate` que tem uma implementação padrão, o equivalente a um método virtual .NET Framework.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3403.fs)]

O exemplo a seguir ilustra uma classe derivada que substitui um método de classe base. Nesse caso, a substituição altera o comportamento para que o método não faça nada.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3404.fs)]

## <a name="overloaded-methods"></a>Métodos sobrecarregados

Métodos sobrecarregados são métodos que têm nomes idênticos em um determinado tipo, mas que têm argumentos diferentes. Em F #, os argumentos opcionais geralmente são usados em vez de métodos sobrecarregados. No entanto, os métodos sobrecarregados são permitidos na linguagem, desde que os argumentos estejam no formato de tupla, não no formulário na forma curried.

## <a name="optional-arguments"></a>Argumentos opcionais

A partir do F # 4,1, você também pode ter argumentos opcionais com um valor de parâmetro padrão em métodos.  Isso é para ajudar a facilitar a interoperação com o código C#.  O exemplo a seguir demonstra a sintaxe:

```fsharp
// A class with a method M, which takes in an optional integer argument.
type C() =
    _.M([<Optional; DefaultParameterValue(12)>] i) = i + 1
```

Observe que o valor passado para `DefaultParameterValue` deve corresponder ao tipo de entrada.  No exemplo acima, é um `int` .  A tentativa de passar um valor não inteiro em `DefaultParameterValue` resultaria em um erro de compilação.

## <a name="example-properties-and-methods"></a>Exemplo: propriedades e métodos

O exemplo a seguir contém um tipo que tem exemplos de campos, funções particulares, propriedades e um método estático.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3406.fs)]

## <a name="see-also"></a>Confira também

- [Membros](index.md)
