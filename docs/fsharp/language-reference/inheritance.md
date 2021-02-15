---
title: Herança
description: "Saiba como especificar relações de herança de F # usando a palavra-chave ' Inherit '."
ms.date: 05/16/2016
ms.openlocfilehash: 5ab891a93528427a66e4eb8f7bfeccbf6e4d2c7e
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223843"
---
# <a name="inheritance"></a>Herança

A herança é usada para modelar a relação "is-a" ou subdigitação, em programação orientada a objeto.

## <a name="specifying-inheritance-relationships"></a>Especificando relações de herança

Você especifica relações de herança usando a `inherit` palavra-chave em uma declaração de classe. O formulário sintático básico é mostrado no exemplo a seguir.

```fsharp
type MyDerived(...) =
    inherit MyBase(...)
```

Uma classe pode ter no máximo uma classe base direta. Se você não especificar uma classe base usando a `inherit` palavra-chave, a classe herdará implicitamente de `System.Object` .

## <a name="inherited-members"></a>Membros herdados

Se uma classe herdar de outra classe, os métodos e os membros da classe base estarão disponíveis para os usuários da classe derivada como se fossem membros diretos da classe derivada.

Qualquer associação de Let e parâmetros de Construtor são privados a uma classe e, portanto, não podem ser acessados de classes derivadas.

A palavra-chave `base` está disponível em classes derivadas e refere-se à instância da classe base. Ele é usado como o autoidentifier.

## <a name="virtual-methods-and-overrides"></a>Métodos virtuais e substituições

Métodos virtuais (e propriedades) funcionam de maneira um pouco diferente em F # em comparação com outras linguagens .NET. Para declarar um novo membro virtual, use a `abstract` palavra-chave. Você faz isso, independentemente de fornecer uma implementação padrão para esse método. Portanto, uma definição completa de um método virtual em uma classe base segue esse padrão:

```fsharp
abstract member [method-name] : [type]

default [self-identifier].[method-name] [argument-list] = [method-body]
```

E em uma classe derivada, uma substituição desse método virtual segue esse padrão:

```fsharp
override [self-identifier].[method-name] [argument-list] = [method-body]
```

Se você omitir a implementação padrão na classe base, a classe base se tornará uma classe abstrata.

O exemplo de código a seguir ilustra a declaração de um novo método virtual `function1` em uma classe base e como substituí-lo em uma classe derivada.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2601.fs)]

## <a name="constructors-and-inheritance"></a>Construtores e herança

O construtor para a classe base deve ser chamado na classe derivada. Os argumentos para o construtor da classe base aparecem na lista de argumentos na `inherit` cláusula. Os valores que são usados devem ser determinados a partir dos argumentos fornecidos para o construtor de classe derivada.

O código a seguir mostra uma classe base e uma classe derivada, em que a classe derivada chama o construtor da classe base na cláusula Inherit:

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2602.fs)]

No caso de vários construtores, o código a seguir pode ser usado. A primeira linha dos construtores da classe derivada é a `inherit` cláusula e os campos são exibidos como campos explícitos declarados com a `val` palavra-chave. Para obter mais informações, consulte [campos explícitos: a `val` palavra-chave](./members/explicit-fields-the-val-keyword.md).

```fsharp
type BaseClass =
    val string1 : string
    new (str) = { string1 = str }
    new () = { string1 = "" }

type DerivedClass =
    inherit BaseClass

    val string2 : string
    new (str1, str2) = { inherit BaseClass(str1); string2 = str2 }
    new (str2) = { inherit BaseClass(); string2 = str2 }

let obj1 = DerivedClass("A", "B")
let obj2 = DerivedClass("A")
```

## <a name="alternatives-to-inheritance"></a>Alternativas à herança

Nos casos em que uma modificação secundária de um tipo é necessária, considere usar uma expressão de objeto como uma alternativa à herança. O exemplo a seguir ilustra o uso de uma expressão de objeto como uma alternativa para criar um novo tipo derivado:

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2603.fs)]

Para obter mais informações sobre expressões de objeto, consulte [expressões de objeto](object-expressions.md).

Ao criar hierarquias de objeto, considere usar uma união discriminada em vez de herança. Uniões discriminadas também podem modelar comportamentos variados de diferentes objetos que compartilham um tipo geral comum. Uma única união discriminada pode, muitas vezes, eliminar a necessidade de várias classes derivadas que são pequenas variações umas das outras. Para obter informações sobre uniões discriminadas, consulte [uniões discriminadas](discriminated-unions.md).

## <a name="see-also"></a>Confira também

- [Expressões de objeto](object-expressions.md)
- [Referência de linguagem F #](index.md)
