---
title: Propriedades
description: 'Saiba mais sobre as propriedades de F #, que são membros que representam valores associados a um objeto.'
ms.date: 05/16/2016
ms.openlocfilehash: a2a4fbfc88831dcb5cad7a2da701969b2e98b2e3
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740192"
---
# <a name="properties"></a>Propriedades

*As propriedades* são membros que representam valores associados a um objeto.

## <a name="syntax"></a>Sintaxe

```fsharp
// Property that has both get and set defined.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with [accessibility-modifier] get() =
    get-function-body
and [accessibility-modifier] set parameter =
    set-function-body

// Alternative syntax for a property that has get and set.
[ attributes-for-get ]
[ static ] member [accessibility-modifier-for-get] [self-identifier.]PropertyName =
    get-function-body
[ attributes-for-set ]
[ static ] member [accessibility-modifier-for-set] [self-identifier.]PropertyName
with set parameter =
    set-function-body

// Property that has get only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName =
    get-function-body

// Alternative syntax for property that has get only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with get() =
    get-function-body

// Property that has set only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with set parameter =
    set-function-body

// Automatically implemented properties.
[ attributes ]
[ static ] member val [accessibility-modifier] PropertyName = initialization-expression [ with get, set ]
```

## <a name="remarks"></a>Comentários

As propriedades representam a relação "tem um" na programação orientada a objeto, representando os dados associados a instâncias de objeto ou, para propriedades estáticas, com o tipo.

Você pode declarar Propriedades de duas maneiras, dependendo se você deseja especificar explicitamente o valor subjacente (também chamado de armazenamento de backup) para a propriedade ou se deseja permitir que o compilador gere automaticamente o repositório de backup para você. Em geral, você deve usar a maneira mais explícita se a propriedade tiver uma implementação não trivial e a maneira automática quando a propriedade for apenas um wrapper simples para um valor ou variável. Para declarar uma propriedade explicitamente, use a `member` palavra-chave. Essa sintaxe declarativa é seguida pela sintaxe que especifica os `get` métodos e `set` , também *acessadores* nomeados. As várias formas da sintaxe explícita mostradas na seção sintaxe são usadas para propriedades de leitura/gravação, somente leitura e somente gravação. Para propriedades somente leitura, você define apenas um `get` método; para propriedades somente gravação, defina apenas um `set` método. Observe que, quando uma propriedade tem ambos `get` e `set` acessadores, a sintaxe alternativa permite que você especifique atributos e modificadores de acessibilidade que são diferentes para cada acessador, como é mostrado no código a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3201.fs)]

Para propriedades de leitura/gravação, que têm um `get` `set` método and, a ordem de `get` e `set` pode ser revertida. Como alternativa, você pode fornecer a sintaxe mostrada `get` apenas para e a sintaxe mostrada `set` apenas em vez de usar a sintaxe combinada. Isso torna mais fácil comentar o indivíduo `get` ou o `set` método, se isso for algo que talvez seja necessário fazer. Essa alternativa ao uso da sintaxe combinada é mostrada no código a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3203.fs)]

Os valores privados que contêm os dados para propriedades são chamados de *armazenamentos de backup*. Para que o compilador crie o armazenamento de backup automaticamente, use as palavras-chave `member val` , omita o autoidentificador e, em seguida, forneça uma expressão para inicializar a propriedade. Se a propriedade for mutável, inclua `with get, set` . Por exemplo, o tipo de classe a seguir inclui duas propriedades implementadas automaticamente. `Property1` é somente leitura e é inicializado para o argumento fornecido para o construtor primário e `Property2` é uma propriedade configurável inicializada para uma cadeia de caracteres vazia:

```fsharp
type MyClass(property1 : int) =
member val Property1 = property1
member val Property2 = "" with get, set
```

As propriedades implementadas automaticamente fazem parte da inicialização de um tipo, portanto, elas devem ser incluídas antes de qualquer outra definição de membro, assim como `let` associações e `do` associações em uma definição de tipo. Observe que a expressão que Inicializa uma propriedade implementada automaticamente só é avaliada na inicialização, e não toda vez que a propriedade é acessada. Esse comportamento está em contraste com o comportamento de uma propriedade explicitamente implementada. O que isso significa efetivamente é que o código para inicializar essas propriedades é adicionado ao construtor de uma classe. Considere o seguinte código que mostra essa diferença:

```fsharp
type MyClass() =
    let random  = new System.Random()
    member val AutoProperty = random.Next() with get, set
    member this.ExplicitProperty = random.Next()

let class1 = new MyClass()

printfn $"class1.AutoProperty = %d{class1.AutoProperty}"
printfn $"class1.ExplicitProperty = %d{class1.ExplicitProperty}"
```

**Saída**

```console
class1.AutoProperty = 1853799794
class1.AutoProperty = 1853799794
class1.ExplicitProperty = 978922705
class1.ExplicitProperty = 1131210765
```

A saída do código anterior mostra que o valor de autoproperty é inalterado quando chamado repetidamente, enquanto o Explicitproperty muda a cada vez que é chamado. Isso demonstra que a expressão para uma propriedade implementada automaticamente não é avaliada a cada vez, como é o método getter para a propriedade explícita.

>[!WARNING]
>Há algumas bibliotecas, como a Entity Framework ( `System.Data.Entity` ) que executam operações personalizadas em construtores de classe base que não funcionam bem com a inicialização de propriedades implementadas automaticamente. Nesses casos, tente usar propriedades explícitas.

As propriedades podem ser membros de classes, estruturas, uniões discriminadas, registros, interfaces e extensões de tipo e também podem ser definidas em expressões de objeto.

Atributos podem ser aplicados a propriedades. Para aplicar um atributo a uma propriedade, grave o atributo em uma linha separada antes da propriedade. Para obter mais informações, consulte [Atributos](../attributes.md).

Por padrão, as propriedades são públicas. Os modificadores de acessibilidade também podem ser aplicados às propriedades. Para aplicar um modificador de acessibilidade, adicione-o imediatamente antes do nome da propriedade se ela for para ser aplicada aos `get` `set` métodos e; adicione-o antes `get` das `set` palavras-chave e se for necessária uma acessibilidade diferente para cada acessador. O *modificador de acessibilidade* pode ser um dos seguintes: `public` , `private` , `internal` . Para mais informações, consulte [Controle de acesso](../access-control.md).

Implementações de propriedade são executadas cada vez que uma propriedade é acessada.

## <a name="static-and-instance-properties"></a>Propriedades de instância e estática

As propriedades podem ser propriedades estáticas ou de instância. As propriedades estáticas podem ser chamadas sem uma instância e são usadas para valores associados ao tipo, não com objetos individuais. Para propriedades estáticas, omita o próprio identificador. O autoidentificador é necessário para as propriedades de instância.

A definição de propriedade estática a seguir se baseia em um cenário no qual você tem um campo estático `myStaticValue` que é o repositório de backup para a propriedade.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3204.fs)]

As propriedades também podem ser do tipo matriz; nesse caso, elas são chamadas de *Propriedades indexadas*. Para obter mais informações, consulte [Propriedades indexadas](indexed-properties.md).

## <a name="type-annotation-for-properties"></a>Digitar anotação para propriedades

Em muitos casos, o compilador tem informações suficientes para inferir o tipo de uma propriedade do tipo de armazenamento de backup, mas você pode definir o tipo explicitamente adicionando uma anotação de tipo.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3205.fs)]

## <a name="using-property-set-accessors"></a>Usando acessadores de conjunto de propriedades

Você pode definir propriedades que fornecem `set` acessadores usando o `<-` operador.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3206.fs)]

A saída é **20**.

## <a name="abstract-properties"></a>Propriedades abstratas

As propriedades podem ser abstratas. Assim como acontece com métodos, `abstract` apenas significa que há um despacho virtual associado à propriedade. As propriedades abstratas podem ser realmente abstratas, ou seja, sem uma definição na mesma classe. A classe que contém essa propriedade é, portanto, uma classe abstrata. Como alternativa, abstract pode significar apenas que uma propriedade é virtual e, nesse caso, uma definição deve estar presente na mesma classe. Observe que as propriedades abstratas não devem ser particulares e, se um acessador for abstrato, o outro também deverá ser abstrato. Para obter mais informações sobre classes abstratas, consulte [classes abstratas](../abstract-classes.md).

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3207.fs)]

## <a name="see-also"></a>Confira também

- [Membros](index.md)
- [Métodos](methods.md)
