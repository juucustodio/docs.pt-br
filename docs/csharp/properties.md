---
title: Propriedades
description: Saiba mais sobre propriedades C#, que incluem recursos de validação, valores computados, avaliação lenta e notificações de alteração de propriedade.
ms.technology: csharp-fundamentals
ms.date: 04/25/2018
ms.openlocfilehash: 5306650a10a3de0ff208f7c72c0ba520a527e746
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437939"
---
# <a name="properties"></a>Propriedades

As propriedades são cidadãos de primeira classe no C#. A linguagem define uma sintaxe que permite aos desenvolvedores escrever código que expresse sua intenção de design com precisão.

As propriedades se comportam como campos quando são acessadas.
No entanto, diferentemente dos campos, as propriedades são implementadas com acessadores, que definem as instruções que são executadas quando uma propriedade é acessada ou atribuída.

## <a name="property-syntax"></a>Sintaxe de propriedade

A sintaxe para propriedades é uma extensão natural para os campos. Um campo define um local de armazenamento:

[!code-csharp[Person class with public fields](../../samples/snippets/csharp/properties/Person.cs#1)]

Uma definição de propriedade contém declarações para um acessador `get` e `set` que recupera e atribui o valor dessa propriedade:

[!code-csharp[Person class with public properties](../../samples/snippets/csharp/properties/Person.cs#2)]

A sintaxe mostrada acima é a sintaxe da *propriedade automática*. O compilador gera o local de armazenamento para o campo que dá suporte à propriedade. O compilador também implementa o corpo dos acessadores `get` e `set`.

Às vezes, você precisa inicializar uma propriedade para um valor diferente do padrão para seu tipo.  O C# permite isso definindo um valor após a chave de fechamento da propriedade. Você pode preferir que o valor inicial para a propriedade `FirstName` seja a cadeia de caracteres vazia em vez de `null`. Você deve especificar isso conforme mostrado abaixo:

[!code-csharp[Person class with properties and initializer](../../samples/snippets/csharp/properties/Person.cs#3)]

A inicialização específica é mais útil para propriedades somente leitura, como você verá adiante neste artigo.

Você mesmo também pode definir o armazenamento, conforme mostrado abaixo:

[!code-csharp[Person class with properties and backing field](../../samples/snippets/csharp/properties/Person.cs#4)]

Quando uma implementação de propriedade é uma única expressão, você pode usar *membros aptos para expressão* para o getter ou setter:

[!code-csharp[Person class with properties and expression bodied getters and setters](../../samples/snippets/csharp/properties/Person.cs#5)]

Essa sintaxe simplificada será usada quando aplicável ao longo deste artigo.

A definição da propriedade mostrada acima é uma propriedade de leitura/gravação. Observe a palavra-chave `value` no acessador set. O acessador `set` sempre tem um parâmetro único chamado `value`. O acessador `get` deve retornar um valor que seja conversível para o tipo da propriedade (`string`, neste exemplo).

Essas são as noções básicas sobre a sintaxe. Há muitas variações diferentes que oferecem suporte a uma variedade de linguagens de design diferentes. Vamos explorá-las e conhecer as opções de sintaxe para cada uma.

## <a name="scenarios"></a>Cenários

Os exemplos acima mostraram um dos casos mais simples de definição de propriedade: uma propriedade de leitura/gravação sem validação. Ao escrever o código que você deseja nos acessadores `get` e `set`, você pode criar vários cenários diferentes.

### <a name="validation"></a>Validação

Você pode escrever código no acessador `set` para garantir que os valores representados por uma propriedade sejam sempre válidos. Por exemplo, suponha que uma regra para a classe `Person` é que o nome não pode ser um espaço em branco. Você escreveria isso da seguinte maneira:

[!code-csharp[Validating property setters](../../samples/snippets/csharp/properties/Person.cs#6)]

O exemplo anterior pode ser simplificado usando uma `throw` expressão como parte da validação de setter de propriedade:

[!code-csharp[Validating property setters](../../samples/snippets/csharp/properties/Person.cs#7)]

O exemplo acima aplica a regra de que o nome não pode ser em branco ou espaço em branco. Se um desenvolvedor escreve

```csharp
hero.FirstName = "";
```

Essa atribuição lança uma `ArgumentException`. Como um acessador set de propriedade deve ter um tipo de retorno void, você relata erros no acessador set lançando uma exceção.

Você pode estender essa mesma sintaxe para qualquer coisa necessária em seu cenário. Você pode verificar as relações entre diferentes propriedades ou validar em relação a qualquer condição externa. Todas as instruções de C# válidas são válidas em um acessador de propriedade.

### <a name="read-only"></a>Somente leitura

Até aqui, todas as definições de propriedade que você viu são de propriedades de leitura/gravação com acessadores públicos. Essa não é a única acessibilidade válida para as propriedades.
Você pode criar propriedades somente leitura ou dar acessibilidade diferente aos acessadores get e set. Suponha que sua classe `Person` só deva habilitar a alteração do valor da propriedade `FirstName` em outros métodos naquela classe. Você pode dar acessibilidade `private` ao acessador set, em vez de `public`:

[!code-csharp[Using a private setter for a publicly readonly property](../../samples/snippets/csharp/properties/Person.cs#8)]

Agora, a propriedade `FirstName` pode ser acessada de qualquer código, mas só pode ser atribuída de outro código na classe `Person`.

Você pode adicionar qualquer modificador de acesso restritivo aos acessadores get ou set. Nenhum modificador de acesso que você colocar no acessador individual deve ser mais limitado que o modificador de acesso da definição de propriedade. O que está acima é válido porque a propriedade `FirstName` é `public`, mas o acessador set é `private`. Você não pode declarar uma propriedade `private` com um acessador `public`. As declarações de propriedade também podem ser declaradas `protected`, `internal`, `protected internal` ou até mesmo `private`.

Também é válido colocar o modificador mais restritivo no acessador `get`. Por exemplo, você poderia ter uma propriedade `public`, mas restringir o acessador `get` como `private`. Esse cenário raramente acontece na prática.

Você também pode restringir modificações a uma propriedade para que ela possa ser definida somente em um construtor ou um inicializador de propriedade. Você pode modificar a classe `Person` da seguinte maneira:

[!code-csharp[A readonly auto implemented property](../../samples/snippets/csharp/properties/Person.cs#9)]

Esse recurso é mais comumente usado para inicializar coleções que são expostas como propriedades somente leitura:

```csharp
public class Measurements
{
    public ICollection<DataPoint> points { get; } = new List<DataPoint>();
}
```

### <a name="computed-properties"></a>Propriedades computadas

Uma propriedade não precisa simplesmente retornar o valor de um campo de membro. Você pode criar propriedades que retornam um valor computado. Vamos expandir o objeto `Person` para retornar o nome completo, computado pela concatenação dos nomes e sobrenomes:

[!code-csharp[A computed property](../../samples/snippets/csharp/properties/Person.cs#10)]

O exemplo acima usa o recurso de [interpolação de cadeia de caracteres](./language-reference/tokens/interpolated.md) para criar a cadeia de caracteres formatada do nome completo.

Use também um *membro com corpo da expressão*, que fornece uma maneira mais sucinta de criar a propriedade `FullName` computada:

[!code-csharp[A computed property using an expression bodied member](../../samples/snippets/csharp/properties/Person.cs#11)]

Os *membros com corpo da expressão* usam a sintaxe *expressão lambda* para definir métodos que contêm uma única expressão. Aqui, essa expressão retorna o nome completo do objeto person.

### <a name="cached-evaluated-properties"></a>Propriedades avaliadas armazenadas em cache

Combine o conceito de uma propriedade computada com o armazenamento e crie uma *propriedade avaliada armazenada em cache*.  Por exemplo, você poderia atualizar a propriedade `FullName` para que a formatação da cadeia de caracteres só acontecesse na primeira vez que ela foi acessada:

[!code-csharp[Caching the value of a computed property](../../samples/snippets/csharp/properties/Person.cs#12)]

No entanto, o código acima contém um bug. Se o código atualizar o valor das propriedades `FirstName` ou `LastName`, o campo `fullName`, anteriormente avaliado, será inválido. Modifique os acessadores `set` das propriedades `FirstName` e `LastName` para que o campo `fullName` seja calculado novamente:

[!code-csharp[Invalidating the cache correctly](../../samples/snippets/csharp/properties/Person.cs#13)]

Esta versão final avalia a propriedade `FullName` apenas quando necessário.
Se a versão calculada anteriormente for válida, ela será usada. Se outra alteração de estado invalidar a versão calculada anteriormente, ela será recalculada. Os desenvolvedores que usam essa classe não precisam saber dos detalhes da implementação. Nenhuma dessas alterações internas afetam o uso do objeto Person. Esse é o motivo principal para o uso de propriedades para expor os membros de dados de um objeto.

### <a name="attaching-attributes-to-auto-implemented-properties"></a>Anexando atributos a propriedades autoimplementadas

Do C# 7.3 em diante, atributos de campo podem ser anexados ao campo de suporte gerado pelo compilador em propriedades autoimplementadas. Por exemplo, considere uma revisão da classe `Person` que adiciona uma propriedade `Id` de inteiro exclusivo.
Você escreve a `Id` propriedade usando uma propriedade implementada automaticamente, mas o design não chama a propriedade de persistência `Id` . O <xref:System.NonSerializedAttribute> pode ser anexado apenas a campos, não a propriedades. Anexe o <xref:System.NonSerializedAttribute> ao campo de suporte da propriedade `Id` usando o especificador `field:` no atributo, conforme mostrado no seguinte exemplo:

[!code-csharp[Attaching attributes to a backing field](../../samples/snippets/csharp/properties/Person.cs#14)]

Essa técnica funciona para qualquer atributo anexado ao campo de suporte na propriedade autoimplementada.

### <a name="implementing-inotifypropertychanged"></a>Implementando INotifyPropertyChanged

A última situação em que você precisa escrever código em um acessador de propriedade é para oferecer suporte à interface <xref:System.ComponentModel.INotifyPropertyChanged>, usada para notificar os clientes de vinculação de dados que um valor foi alterado. Quando o valor de uma propriedade for alterado, o objeto aciona o evento <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged?displayProperty=nameWithType> para indicar a alteração. As bibliotecas de vinculação de dados, por sua vez, atualizam os elementos de exibição com base nessa alteração. O código a seguir mostra como você implementaria `INotifyPropertyChanged` para a propriedade `FirstName` dessa classe person.

[!code-csharp[invalidating the cache correctly](../../samples/snippets/csharp/properties/Person.cs#15)]

O operador `?.` é chamado de *operador condicional nulo*. Ele verifica uma referência nula antes de avaliar o lado direito do operador. O resultado final é que, se não houver nenhum assinante para o evento `PropertyChanged`, o código para acionar o evento não é executado. Ela lançaria uma `NullReferenceException` sem essa verificação, nesse caso. Para obter mais informações, confira [`events`](events-overview.md). Este exemplo também usa o novo operador `nameof` para converter o símbolo de nome da propriedade em sua representação de texto.
O uso de `nameof` pode reduzir erros no local em que você digitou errado o nome da propriedade.

Novamente, a implementação de <xref:System.ComponentModel.INotifyPropertyChanged> é um exemplo de um caso em que você pode escrever o código nos acessadores para dar suporte aos cenários necessários.

## <a name="summing-up"></a>Resumindo

As propriedades são uma forma de campos inteligentes em uma classe ou objeto. De fora do objeto, elas parecem como campos no objeto. No entanto, as propriedades podem ser implementadas usando a paleta completa de funcionalidades do C#.
Você pode fornecer validação, acessibilidade diferente, avaliação lenta ou quaisquer requisitos necessários aos seus cenários.
