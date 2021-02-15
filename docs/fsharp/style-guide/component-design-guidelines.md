---
title: Diretrizes de design de componente do F#
description: 'Conheça as diretrizes para escrever componentes F # destinados para consumo por outros chamadores.'
ms.date: 05/14/2018
ms.openlocfilehash: 24be2a422c97b9334f749e3d9dfcccd0feec219b
ms.sourcegitcommit: e395fabeeea5c705d243d246fa64446839ac85b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2021
ms.locfileid: "97856101"
---
# <a name="f-component-design-guidelines"></a>Diretrizes de design de componente do F#

Este documento é um conjunto de diretrizes de design de componentes para programação em F #, com base nas diretrizes de design de componente F #, v14, Microsoft Research e uma versão que foi originalmente organizada e mantida pelo F # Software Foundation.

Este documento pressupõe que você esteja familiarizado com a programação em F #. Muitos agradecimentos à comunidade do F # por suas contribuições e comentários úteis sobre várias versões deste guia.

## <a name="overview"></a>Visão geral

Este documento analisa alguns dos problemas relacionados ao design e à codificação de componentes do F #. Um componente pode significar qualquer um dos seguintes:

* Uma camada em seu projeto F # que tem consumidores externos dentro desse projeto.
* Uma biblioteca destinada ao consumo pelo código F # nos limites do assembly.
* Uma biblioteca destinada ao consumo por qualquer linguagem .NET entre limites de assembly.
* Uma biblioteca destinada à distribuição por meio de um repositório de pacotes, como o [NuGet](https://nuget.org).

As técnicas descritas neste artigo seguem os [cinco princípios de um bom código F #](index.md#five-principles-of-good-f-code)e, portanto, utilizam a programação funcional e de objeto conforme apropriado.

Independentemente da metodologia, o componente e o designer de biblioteca enfrentam vários problemas práticos e prosaicass ao tentar criar uma API que seja mais fácil de ser usada pelos desenvolvedores. A aplicação do Conscientious das [diretrizes de design da biblioteca do .net](../../standard/design-guidelines/index.md) orientará você na criação de um conjunto consistente de APIs que são agradáveis de consumir.

## <a name="general-guidelines"></a>Diretrizes gerais

Há algumas diretrizes universais que se aplicam a bibliotecas F #, independentemente do público-alvo da biblioteca.

### <a name="learn-the-net-library-design-guidelines"></a>Conheça as diretrizes de design de biblioteca do .NET

Independentemente do tipo de codificação F # que você está fazendo, é importante ter um conhecimento prático das [diretrizes de design da biblioteca do .net](../../standard/design-guidelines/index.md). A maioria dos outros programadores F # e .NET estará familiarizado com essas diretrizes e esperará que o código .NET esteja em conformidade com eles.

As diretrizes de design de biblioteca do .NET fornecem orientação geral sobre Nomenclatura, criação de classes e interfaces, design de Membros (Propriedades, métodos, eventos, etc.) e muito mais, e são um ponto de referência útil para uma variedade de diretrizes de design.

### <a name="add-xml-documentation-comments-to-your-code"></a>Adicionar comentários de documentação XML ao seu código

A documentação XML em APIs públicas garante que os usuários possam obter excelentes IntelliSense e Quickinfo ao usar esses tipos e membros e habilitar a criação de arquivos de documentação para a biblioteca. Consulte a [documentação XML](../language-reference/xml-documentation.md) sobre várias marcas XML que podem ser usadas para marcação adicional nos comentários do xmlDoc.

```fsharp
/// A class for representing (x,y) coordinates
type Point =

    /// Computes the distance between this point and another
    member DistanceTo: otherPoint:Point -> float
```

Você pode usar os comentários XML de forma abreviada ( `/// comment` ) ou os comentários XML padrão ( `///<summary>comment</summary>` ).

### <a name="consider-using-explicit-signature-files-fsi-for-stable-library-and-component-apis"></a>Considere o uso de arquivos de assinatura explícitos (. FSI) para APIs estáveis de biblioteca e componente

O uso de arquivos de assinaturas explícitas em uma biblioteca F # fornece um resumo sucinta da API pública, que ajuda a garantir que você conheça a superfície pública completa da biblioteca e fornece uma separação clara entre a documentação pública e os detalhes de implementação interna. Os arquivos de assinatura adicionam o conflito à alteração da API pública, exigindo que sejam feitas alterações nos arquivos de implementação e de assinatura. Como resultado, os arquivos de assinatura normalmente devem ser introduzidos apenas quando uma API se tornar solidificou e não se esperar mais mudar significativamente.

### <a name="always-follow-best-practices-for-using-strings-in-net"></a>Sempre siga as práticas recomendadas para usar cadeias de caracteres no .NET

Siga [as práticas recomendadas para usar cadeias de caracteres em diretrizes .net](../../standard/base-types/best-practices-strings.md) . Em particular, sempre declare explicitamente a *intenção cultural* na conversão e na comparação de cadeias de caracteres (quando aplicável).

## <a name="guidelines-for-f-facing-libraries"></a>Diretrizes para bibliotecas voltadas para o F #

Esta seção apresenta as recomendações para o desenvolvimento de bibliotecas públicas do F #; ou seja, bibliotecas que expõem APIs públicas que devem ser consumidas por desenvolvedores de F #. Há uma variedade de recomendações de design de biblioteca aplicáveis especificamente ao F #. Na ausência das recomendações específicas que se seguem, as diretrizes de design da biblioteca do .NET são as orientações de fallback.

### <a name="naming-conventions"></a>Convenções de nomenclatura

#### <a name="use-net-naming-and-capitalization-conventions"></a>Usar convenções de nomenclatura e uso do .NET

A tabela a seguir segue as convenções de nomenclatura e de capitalização do .NET. Há pequenas adições a também incluem construções F #.

| Constructo | Caixa | Parte | Exemplos | Observações |
|-----------|------|------|----------|-------|
| Tipos concretos | PascalCase | Substantivo/adjetivo | Lista, dupla, complexa | Os tipos concretos são structs, classes, enumerações, delegados, registros e uniões. Embora os nomes de tipo sejam tradicionalmente minúsculos em OCaml, o F # adotou o esquema de nomenclatura .NET para tipos.
| DLLs           | PascalCase |                 | Fabrikam.Core.dll |  |
| Marcas Union     | PascalCase | Substantivo | Alguns, adicionar, sucesso | Não use um prefixo em APIs públicas. Opcionalmente, use um prefixo quando interno, como `type Teams = TAlpha | TBeta | TDelta.` |
| Evento          | PascalCase | Verbo | ValueChanged/ValueChanging |  |
| Exceções     | PascalCase |      | WebException | O nome deve terminar com "Exception". |
| Campo          | PascalCase | Substantivo | CurrentName  | |
| Tipos de interface |  PascalCase | Substantivo/adjetivo | IDisposable | O nome deve começar com "I". |
| Método |  PascalCase |  Verbo | ToString | |
| Namespace | PascalCase | | Microsoft. FSharp. Core | Geralmente `<Organization>.<Technology>[.<Subnamespace>]` , use, embora descarte a organização, se a tecnologia for independente da organização. |
| Parâmetros | camelCase | Substantivo |  typeName, transformar, intervalo | |
| permitir valores (internos) | camelCase ou PascalCase | Substantivo/verbo |  GetValue, myTable |
| permitir valores (externos) | camelCase ou PascalCase | Substantivo/verbo  | Lista. map, datas. hoje | os valores de Let associados são geralmente públicos quando os padrões de design funcional tradicionais são os seguintes. No entanto, geralmente use PascalCase quando o identificador puder ser usado de outras linguagens .NET. |
| Propriedade  | PascalCase  | Substantivo/adjetivo  | IsEndOfFile, BackColor  | As propriedades boolianas geralmente usam e podem e devem ser afirmativo, como em IsEndOfFile, e não IsNotEndOfFile.

#### <a name="avoid-abbreviations"></a>Evitar abreviações

As diretrizes do .NET desestimulam o uso de abreviações (por exemplo, "uso `OnButtonClick` em vez de `OnBtnClick` "). Abreviações comuns, como `Async` para "Asynchronous", são toleradas. Essa diretriz é, às vezes, ignorada para a programação funcional; por exemplo, `List.iter` usa uma abreviação para "iterar". Por esse motivo, o uso de abreviações tende a ser tolerado a um grau maior na programação F #-to-F #, mas ainda deve ser evitado em geral no design de componentes públicos.

#### <a name="avoid-casing-name-collisions"></a>Evitar colisões de nome com maiúsculas e minúsculas

As diretrizes do .NET dizem que o uso de maiúsculas e minúsculas não pode ser usado para desambiguar colisões de nomes, pois alguns idiomas de cliente (por exemplo, Visual Basic) não diferenciam maiúsculas de minúsculas.

#### <a name="use-acronyms-where-appropriate"></a>Use acrônimos quando apropriado

Acrônimos como XML não são abreviações e são amplamente usados em bibliotecas .NET em formato não capitalizado (XML). Apenas acrônimos conhecidos e amplamente reconhecidos devem ser usados.

#### <a name="use-pascalcase-for-generic-parameter-names"></a>Usar PascalCase para nomes de parâmetro genéricos

Use PascalCase para nomes de parâmetro genéricos em APIs públicas, incluindo as bibliotecas voltadas para o F #. Em particular, use nomes como `T` , `U` , `T1` , `T2` para parâmetros genéricos arbitrários e quando nomes específicos fizerem sentido; em seguida, para bibliotecas em F #, use nomes como `Key` , `Value` , `Arg` mas não por exemplo, `TKey` ).

#### <a name="use-either-pascalcase-or-camelcase-for-public-functions-and-values-in-f-modules"></a>Usar PascalCase ou camelCase para funções e valores públicos em módulos F #

camelCase é usado para funções públicas que são projetadas para serem usadas não qualificadas (por exemplo, `invalidArg` ) e para as "funções de coleção padrão" (por exemplo, List. map). Em ambos os casos, os nomes de função funcionam de forma muito parecida com palavras-chave no idioma.

### <a name="object-type-and-module-design"></a>Design de objeto, tipo e módulo

#### <a name="use-namespaces-or-modules-to-contain-your-types-and-modules"></a>Usar namespaces ou módulos para conter seus tipos e módulos

Cada arquivo F # em um componente deve começar com uma declaração de namespace ou uma declaração de módulo.

```fsharp
namespace Fabrikam.BasicOperationsAndTypes

type ObjectType1() =
    ...

type ObjectType2() =
     ...

module CommonOperations =
    ...
```

ou

```fsharp
module Fabrikam.BasicOperationsAndTypes

type ObjectType1() =
    ...

type ObjectType2() =
    ...

module CommonOperations =
    ...
```

As diferenças entre usar módulos e namespaces para organizar o código no nível superior são as seguintes:

* Namespaces podem abranger vários arquivos
* Namespaces não podem conter funções F #, a menos que estejam dentro de um módulo interno
* O código para qualquer módulo fornecido deve estar contido em um único arquivo
* Módulos de nível superior podem conter funções F # sem a necessidade de um módulo interno

A escolha entre um namespace ou módulo de nível superior afeta a forma compilada do código e, portanto, afetará a exibição de outras linguagens do .NET caso sua API seja eventualmente consumida fora do código F #.

#### <a name="use-methods-and-properties-for-operations-intrinsic-to-object-types"></a>Usar métodos e propriedades para operações intrínsecas a tipos de objeto

Ao trabalhar com objetos, é melhor garantir que a funcionalidade de consumo seja implementada como métodos e propriedades nesse tipo.

```fsharp
type HardwareDevice() =

    member this.ID = ...

    member this.SupportedProtocols = ...

type HashTable<'Key,'Value>(comparer: IEqualityComparer<'Key>) =

    member this.Add(key, value) = ...

    member this.ContainsKey(key) = ...

    member this.ContainsValue(value) = ...
```

A maior parte da funcionalidade para um determinado membro não precisa necessariamente ser implementada nesse membro, mas a parte consumível dessa funcionalidade deve ser.

#### <a name="use-classes-to-encapsulate-mutable-state"></a>Usar classes para encapsular o estado mutável

Em F #, isso só precisa ser feito quando esse estado ainda não é encapsulado por outro constructo de linguagem, como um fechamento, uma expressão de sequência ou uma computação assíncrona.

```fsharp
type Counter() =
    // let-bound values are private in classes.
    let mutable count = 0

    member this.Next() =
        count <- count + 1
        count
```

#### <a name="use-interfaces-to-group-related-operations"></a>Usar interfaces para agrupar operações relacionadas

Use tipos de interface para representar um conjunto de operações. Isso é preferível a outras opções, como tuplas de funções ou registros de funções.

```fsharp
type Serializer =
    abstract Serialize<'T> : preserveRefEq: bool -> value: 'T -> string
    abstract Deserialize<'T> : preserveRefEq: bool -> pickle: string -> 'T
```

Em preferência a:

```fsharp
type Serializer<'T> = {
    Serialize: bool -> 'T -> string
    Deserialize: bool -> string -> 'T
}
```

As interfaces são conceitos de primeira classe no .NET, que você pode usar para obter o que o transmissão functors normalmente daria a você. Além disso, eles podem ser usados para codificar tipos Existential em seu programa, quais registros de funções não podem.

#### <a name="use-a-module-to-group-functions-that-act-on-collections"></a>Usar um módulo para agrupar funções que atuam em coleções

Ao definir um tipo de coleção, considere fornecer um conjunto padrão de operações como `CollectionType.map` e `CollectionType.iter` ) para novos tipos de coleção.

```fsharp
module CollectionType =
    let map f c =
        ...
    let iter f c =
        ...
```

Se você incluir esse módulo, siga as convenções de nomenclatura padrão para as funções encontradas no FSharp. Core.

#### <a name="use-a-module-to-group-functions-for-common-canonical-functions-especially-in-math-and-dsl-libraries"></a>Use um módulo para agrupar funções para funções comuns e canônicas, especialmente em bibliotecas de matemática e DSL

Por exemplo, `Microsoft.FSharp.Core.Operators` é uma coleção aberta automaticamente de funções de nível superior (como `abs` e `sin` ) fornecida pelo FSharp.Core.dll.

Da mesma forma, uma biblioteca de estatísticas pode incluir um módulo com funções `erf` e `erfc` , em que esse módulo foi projetado para ser aberto explicitamente ou automaticamente.

#### <a name="consider-using-requirequalifiedaccess-and-carefully-apply-autoopen-attributes"></a>Considere usar RequireQualifiedAccess e aplicar cuidadosamente os atributos AutoOpen

A adição do `[<RequireQualifiedAccess>]` atributo a um módulo indica que o módulo pode não estar aberto e que as referências aos elementos do módulo exigem acesso qualificado explícito. Por exemplo, o `Microsoft.FSharp.Collections.List` módulo tem esse atributo.

Isso é útil quando as funções e os valores no módulo têm nomes que provavelmente estão em conflito com nomes em outros módulos. Exigir acesso qualificado pode aumentar muito a manutenção e o evolucionabilidade de longo prazo de uma biblioteca.

Adicionar o `[<AutoOpen>]` atributo a um módulo significa que o módulo será aberto quando o namespace recipiente for aberto. O `[<AutoOpen>]` atributo também pode ser aplicado a um assembly para indicar um módulo que é aberto automaticamente quando o assembly é referenciado.

Por exemplo, uma biblioteca de estatísticas **MathsHeaven. Statistics** pode conter `module MathsHeaven.Statistics.Operators` funções contendo `erf` e `erfc` . É razoável marcar esse módulo como `[<AutoOpen>]` . Isso significa `open MathsHeaven.Statistics` também abrir esse módulo e colocar os nomes `erf` e o `erfc` escopo. Outro bom uso do `[<AutoOpen>]` é para módulos que contêm métodos de extensão.

O uso excessivo de `[<AutoOpen>]` clientes potenciais para namespaces poluidos e o atributo deve ser usado com cuidado. Para bibliotecas específicas em domínios específicos, o uso criterioso de `[<AutoOpen>]` pode levar a uma melhor usabilidade.

#### <a name="consider-defining-operator-members-on-classes-where-using-well-known-operators-is-appropriate"></a>Considere definir membros de operador em classes em que o uso de operadores conhecidos é apropriado

Às vezes, as classes são usadas para modelar construções matemáticas, como vetores. Quando o domínio que está sendo modelado tem operadores bem conhecidos, defini-los como membros intrínsecos à classe é útil.

```fsharp
type Vector(x: float) =

    member v.X = x

    static member (*) (vector: Vector, scalar: float) = Vector(vector.X * scalar)

    static member (+) (vector1: Vector, vector2: Vector) = Vector(vector1.X + vector2.X)

let v = Vector(5.0)

let u = v * 10.0
```

Esta orientação corresponde às diretrizes gerais do .NET para esses tipos. No entanto, ele também pode ser importante na codificação F #, pois isso permite que esses tipos sejam usados em conjunto com funções e métodos F # com restrições de membro, como List. sumBy.

#### <a name="consider-using-compiledname-to-provide-a-net-friendly-name-for-other-net-language-consumers"></a>Considere o uso de CompiledName para fornecer um. Nome amigável para rede para outros consumidores de linguagem .NET

Às vezes, talvez você queira nomear algo em um estilo para consumidores de F # (como um membro estático em letras minúsculas para que ele apareça como se fosse uma função associada a um módulo), mas tenha um estilo diferente para o nome quando ele for compilado em um assembly. Você pode usar o `[<CompiledName>]` atributo para fornecer um estilo diferente para o código que não seja F # consumindo o assembly.

```fsharp
type Vector(x:float, y:float) =

    member v.X = x
    member v.Y = y

    [<CompiledName("Create")>]
    static member create x y = Vector (x, y)

let v = Vector.create 5.0 3.0
```

Usando o `[<CompiledName>]` , você pode usar as convenções de nomenclatura do .net para consumidores que não são do F # do assembly.

#### <a name="use-method-overloading-for-member-functions-if-doing-so-provides-a-simpler-api"></a>Use a sobrecarga de método para funções de membro, se isso fornecer uma API mais simples

A sobrecarga do método é uma ferramenta poderosa para simplificar uma API que pode precisar executar uma funcionalidade semelhante, mas com opções ou argumentos diferentes.

```fsharp
type Logger() =

    member this.Log(message) =
        ...
    member this.Log(message, retryPolicy) =
        ...
```

Em F #, é mais comum sobrecarregar o número de argumentos em vez de tipos de argumentos.

#### <a name="hide-the-representations-of-record-and-union-types-if-the-design-of-these-types-is-likely-to-evolve"></a>Oculte as representações de tipos de registro e União se o design desses tipos for provavelmente evoluir

Evite revelar representações concretas de objetos. Por exemplo, a representação concreta dos <xref:System.DateTime> valores não é revelada pela API pública externa do design da biblioteca do .net. Em tempo de execução, o Common Language Runtime sabe a implementação confirmada que será usada durante toda a execução. No entanto, o código compilado não pega as dependências na representação concreta.

#### <a name="avoid-the-use-of-implementation-inheritance-for-extensibility"></a>Evite o uso da herança de implementação para extensibilidade

Em F #, a herança de implementação raramente é usada. Além disso, as hierarquias de herança geralmente são complexas e difíceis de alterar quando novos requisitos chegam. A implementação de herança ainda existe em F # para compatibilidade e casos raros em que é a melhor solução para um problema, mas técnicas alternativas devem ser buscadas em seus programas em F # durante a criação de polimorfismo, como implementação de interface.

### <a name="function-and-member-signatures"></a>Assinaturas de funções e membros

#### <a name="use-tuples-for-return-values-when-returning-a-small-number-of-multiple-unrelated-values"></a>Usar tuplas para valores de retorno ao retornar um pequeno número de vários valores não relacionados

Este é um bom exemplo do uso de uma tupla em um tipo de retorno:

```fsharp
val divrem: BigInteger -> BigInteger -> BigInteger * BigInteger
```

Para tipos de retorno que contêm muitos componentes ou onde os componentes estão relacionados a uma única entidade identificável, considere usar um tipo nomeado em vez de uma tupla.

#### <a name="use-asynct-for-async-programming-at-f-api-boundaries"></a>Usar `Async<T>` para programação assíncrona em limites de API F #

Se houver uma operação síncrona correspondente chamada `Operation` que retorna um `T` , a operação assíncrona deverá ser nomeada `AsyncOperation` se retornar `Async<T>` ou `OperationAsync` se retornar `Task<T>` . Para tipos .NET comumente usados que expõem os métodos Begin/End, considere usar `Async.FromBeginEnd` o para gravar métodos de extensão como uma fachada para fornecer o modelo de programação de F # Async para essas APIs .net.

```fsharp
type SomeType =
    member this.Compute(x:int): int =
        ...
    member this.AsyncCompute(x:int): Async<int> =
        ...

type System.ServiceModel.Channels.IInputChannel with
    member this.AsyncReceive() =
        ...
```

### <a name="exceptions"></a>Exceções

Consulte [Gerenciamento de erros](conventions.md#error-management) para saber mais sobre o uso apropriado de exceções, resultados e opções.

### <a name="extension-members"></a>Membros de extensão

#### <a name="carefully-apply-f-extension-members-in-f-to-f-components"></a>Aplicar cuidadosamente membros de extensão F # em componentes F #-to-F #

Os membros de extensão F # geralmente devem ser usados apenas para operações que estão no fechamento de operações intrínsecas associadas a um tipo na maioria dos seus modos de uso. Um uso comum é fornecer APIs que são mais idiomática a F # para vários tipos .NET:

```fsharp
type System.ServiceModel.Channels.IInputChannel with
    member this.AsyncReceive() =
        Async.FromBeginEnd(this.BeginReceive, this.EndReceive)

type System.Collections.Generic.IDictionary<'Key,'Value> with
    member this.TryGet key =
        let ok, v = this.TryGetValue key
        if ok then Some v else None
```

### <a name="union-types"></a>Tipos de União

#### <a name="use-discriminated-unions-instead-of-class-hierarchies-for-tree-structured-data"></a>Usar uniões discriminadas em vez de hierarquias de classe para dados estruturados em árvore

As estruturas do tipo árvore são definidas recursivamente. Isso é estranho com a herança, mas elegante com uniões discriminadas.

```fsharp
type BST<'T> =
    | Empty
    | Node of 'T * BST<'T> * BST<'T>
```

A representação de dados do tipo árvore com uniões discriminadas também permite que você se beneficie da exaustivaidade na correspondência de padrões.

#### <a name="use-requirequalifiedaccess-on-union-types-whose-case-names-are-not-sufficiently-unique"></a>Use `[<RequireQualifiedAccess>]` em tipos de União cujos nomes de caso não sejam exclusivos o suficiente

Você pode se deparar em um domínio em que o mesmo nome seja o melhor para coisas diferentes, como casos de União discriminados. Você pode usar `[<RequireQualifiedAccess>]` para desambiguar nomes de casos para evitar o disparo de erros confusos devido ao sombreamento dependente da ordem das `open` instruções

#### <a name="hide-the-representations-of-discriminated-unions-for-binary-compatible-apis-if-the-design-of-these-types-is-likely-to-evolve"></a>Ocultar as representações de uniões discriminadas para APIs compatíveis com binários se o design desses tipos for provavelmente evoluir

Tipos de União dependem de formulários de correspondência de padrão F # para um modelo de programação sucinto. Conforme mencionado anteriormente, você deve evitar revelar representações concretas de dados se o design desses tipos for provavelmente evoluir.

Por exemplo, a representação de uma união discriminada pode ser ocultada usando uma declaração privada ou interna, ou usando um arquivo de assinatura.

```fsharp
type Union =
    private
    | CaseA of int
    | CaseB of string
```

Se você revelar as uniões discriminadas indiscriminadamente, poderá achar difícil fazer a versão da biblioteca sem quebrar o código do usuário. Em vez disso, considere revelar um ou mais padrões ativos para permitir a correspondência de padrões sobre os valores de seu tipo.

Os padrões ativos fornecem uma maneira alternativa de fornecer aos consumidores de F # uma correspondência de padrões e, ao mesmo tempo, evitar expor tipos de União F # diretamente.

### <a name="inline-functions-and-member-constraints"></a>Funções embutidas e restrições de membro

#### <a name="define-generic-numeric-algorithms-using-inline-functions-with-implied-member-constraints-and-statically-resolved-generic-types"></a>Definir algoritmos numéricos genéricos usando funções embutidas com restrições de membro implícitas e tipos genéricos resolvidos estaticamente

As restrições de membro aritméticos e as restrições de comparação F # são um padrão para a programação F #. Por exemplo, considere o seguinte código:

```fsharp
let inline highestCommonFactor a b =
    let rec loop a b =
        if a = LanguagePrimitives.GenericZero<_> then b
        elif a < b then loop a (b - a)
        else loop (a - b) b
    loop a b
```

O tipo dessa função é o seguinte:

```fsharp
val inline highestCommonFactor : ^T -> ^T -> ^T
                when ^T : (static member Zero : ^T)
                and ^T : (static member ( - ) : ^T * ^T -> ^T)
                and ^T : equality
                and ^T : comparison
```

Essa é uma função adequada para uma API pública em uma biblioteca matemática.

#### <a name="avoid-using-member-constraints-to-simulate-type-classes-and-duck-typing"></a>Evite usar restrições de membro para simular classes de tipo e digitação pato

É possível simular "digitação pato" usando restrições de membro F #. No entanto, os membros que fazem uso dele não devem ser usados em geral em designs de biblioteca F #-to-F #. Isso ocorre porque os designs de biblioteca baseados em restrições implícitas desconhecidas ou não padrão tendem a fazer com que o código do usuário se torne inflexível e esteja vinculado a um padrão de estrutura específico.

Além disso, há uma boa chance de que o uso intensivo de restrições de membro dessa maneira possa resultar em tempos de compilação muito longos.

### <a name="operator-definitions"></a>Definições de operador

#### <a name="avoid-defining-custom-symbolic-operators"></a>Evite definir operadores simbólicos personalizados

Os operadores personalizados são essenciais em algumas situações e são dispositivos de notação altamente úteis dentro de um grande corpo de código de implementação. Para novos usuários de uma biblioteca, as funções nomeadas costumam ser mais fáceis de usar. Além disso, os operadores simbólicos personalizados podem ser difíceis de documentar e os usuários acham mais difícil procurar ajuda nos operadores, devido a limitações existentes nos mecanismos IDE e de pesquisa.

Como resultado, é melhor publicar sua funcionalidade como funções e membros nomeados e, além disso, expor os operadores para essa funcionalidade somente se os benefícios da notação superarem a documentação e o custo cognitiva de tê-los.

### <a name="units-of-measure"></a>Unidades de medida

#### <a name="carefully-use-units-of-measure-for-added-type-safety-in-f-code"></a>Use cuidadosamente as unidades de medida para a segurança de tipo adicionado no código F #

Informações adicionais de digitação para unidades de medida são apagadas quando exibidas por outras linguagens .NET. Lembre-se de que os componentes, as ferramentas e a reflexão do .NET verão tipos de unidades SANs. Por exemplo, os consumidores do C# verão, `float` em vez de `float<kg>` .

### <a name="type-abbreviations"></a>Abreviações de tipo

#### <a name="carefully-use-type-abbreviations-to-simplify-f-code"></a>Use cuidadosamente abreviações de tipo para simplificar o código F #

Componentes, ferramentas e reflexo do .NET não verão nomes abreviados para tipos. O uso significativo das abreviações de tipo também pode fazer com que um domínio pareça mais complexo do que realmente é, o que poderia confundir os consumidores.

#### <a name="avoid-type-abbreviations-for-public-types-whose-members-and-properties-should-be-intrinsically-different-to-those-available-on-the-type-being-abbreviated"></a>Evite abreviações de tipo para tipos públicos cujos membros e propriedades devam ser intrinsecamente diferentes para aqueles disponíveis no tipo que está sendo abreviado

Nesse caso, o tipo que está sendo abreviado revela muito sobre a representação do tipo real que está sendo definido. Em vez disso, considere encapsular a abreviação em um tipo de classe ou uma união discriminada de caso único (ou, quando o desempenho for essencial, considere usar um tipo de struct para encapsular a abreviação).

Por exemplo, é tentador definir um mapa múltiplo como um caso especial de um mapa F #, por exemplo:

```fsharp
type MultiMap<'Key,'Value> = Map<'Key,'Value list>
```

No entanto, as operações de notação de ponto lógico nesse tipo não são as mesmas que as operações em um mapa – por exemplo, é razoável que o mapa do operador de pesquisa. [chave] retorna a lista vazia se a chave não estiver no dicionário, em vez de gerar uma exceção.

## <a name="guidelines-for-libraries-for-use-from-other-net-languages"></a>Diretrizes para bibliotecas para uso de outras linguagens do .NET

Ao criar bibliotecas para uso de outras linguagens do .NET, é importante aderir às diretrizes de [design da biblioteca do .net](../../standard/design-guidelines/index.md). Neste documento, essas bibliotecas são rotuladas como bibliotecas de .NET da baunilha, em oposição às bibliotecas voltadas para o F # que usam construções F # sem restrição. A criação de bibliotecas .NET da baunilha significa fornecer APIs familiares e idiomática consistentes com o restante dos .NET Framework minimizando o uso de construções específicas de F # na API pública. As regras são explicadas nas seções a seguir.

### <a name="namespace-and-type-design-for-libraries-for-use-from-other-net-languages"></a>Namespace e tipo design (para bibliotecas para uso de outras linguagens .NET)

#### <a name="apply-the-net-naming-conventions-to-the-public-api-of-your-components"></a>Aplicar as convenções de nomenclatura do .NET à API pública de seus componentes

Preste atenção especial ao uso de nomes abreviados e das diretrizes de capitalização do .NET.

```fsharp
type pCoord = ...
    member this.theta = ...

type PolarCoordinate = ...
    member this.Theta = ...
```

#### <a name="use-namespaces-types-and-members-as-the-primary-organizational-structure-for-your-components"></a>Usar namespaces, tipos e membros como a estrutura organizacional principal para seus componentes

Todos os arquivos que contêm a funcionalidade pública devem começar com uma `namespace` declaração e as únicas entidades voltadas para o público em namespaces devem ser tipos. Não use módulos F #.

Use módulos não públicos para manter o código de implementação, tipos de utilitário e funções de utilitário.

Os tipos estáticos devem ser preferidos em relação aos módulos, pois permitem a evolução futura da API usar sobrecarga e outros conceitos de design de API do .NET que não podem ser usados em módulos F #.

Por exemplo, no lugar da seguinte API pública:

```fsharp
module Fabrikam

module Utilities =
    let Name = "Bob"
    let Add2 x y = x + y
    let Add3 x y z = x + y + z
```

Em vez disso, considere:

```fsharp
namespace Fabrikam

[<AbstractClass; Sealed>]
type Utilities =
    static member Name = "Bob"
    static member Add(x,y) = x + y
    static member Add(x,y,z) = x + y + z
```

#### <a name="use-f-record-types-in-vanilla-net-apis-if-the-design-of-the-types-wont-evolve"></a>Use os tipos de registro F # nas APIs do .NET da baunilha se o design dos tipos não evoluir

Os tipos de registro F # são compilados em uma classe .NET simples. Elas são adequadas para alguns tipos simples e estáveis em APIs. Considere o uso `[<NoEquality>]` dos `[<NoComparison>]` atributos e para suprimir a geração automática de interfaces. Além disso, evite usar campos de registro mutáveis nas APIs do .NET da baunilha, pois eles expõem um campo público. Sempre considere se uma classe forneceria uma opção mais flexível para a evolução futura da API.

Por exemplo, o código F # a seguir expõe a API pública para um consumidor de C#:

F#:

```fsharp
[<NoEquality; NoComparison>]
type MyRecord =
    { FirstThing: int
        SecondThing: string }
```

C#:

```csharp
public sealed class MyRecord
{
    public MyRecord(int firstThing, string secondThing);
    public int FirstThing { get; }
    public string SecondThing { get; }
}
```

#### <a name="hide-the-representation-of-f-union-types-in-vanilla-net-apis"></a>Ocultar a representação dos tipos de União F # nas APIs do .NET da baunilha

Tipos de União f # geralmente não são usados em limites de componentes, mesmo para codificação F # para F #. Eles são um dispositivo de implementação excelente quando usados internamente em componentes e bibliotecas.

Ao criar uma API .NET da baunilha, considere ocultar a representação de um tipo Union usando uma declaração particular ou um arquivo de assinatura.

```fsharp
type PropLogic =
    private
    | And of PropLogic * PropLogic
    | Not of PropLogic
    | True
```

Você também pode aumentar os tipos que usam uma representação Union internamente com membros para fornecer um desejado. API voltada para o .net.

```fsharp
type PropLogic =
    private
    | And of PropLogic * PropLogic
    | Not of PropLogic
    | True

    /// A public member for use from C#
    member x.Evaluate =
        match x with
        | And(a,b) -> a.Evaluate && b.Evaluate
        | Not a -> not a.Evaluate
        | True -> true

    /// A public member for use from C#
    static member CreateAnd(a,b) = And(a,b)
```

#### <a name="design-gui-and-other-components-using-the-design-patterns-of-the-framework"></a>Criar GUI e outros componentes usando os padrões de design da estrutura

Há muitas estruturas diferentes disponíveis no .NET, como WinForms, WPF e ASP.NET. As convenções de nomenclatura e design para cada uma devem ser usadas se você estiver criando componentes para uso nessas estruturas. Por exemplo, para a programação do WPF, adote os padrões de design do WPF para as classes que você está projetando. Para modelos na programação de interface do usuário, use padrões de design, como eventos e coleções baseadas em notificação, como aqueles encontrados no <xref:System.Collections.ObjectModel> .

### <a name="object-and-member-design-for-libraries-for-use-from-other-net-languages"></a>Design de objeto e membro (para bibliotecas para uso de outras linguagens do .NET)

#### <a name="use-the-clievent-attribute-to-expose-net-events"></a>Usar o atributo CLIEvent para expor eventos .NET

Construa um `DelegateEvent` com um tipo de delegado .net específico que usa um objeto e `EventArgs` (em vez de um `Event` , que usa apenas o `FSharpHandler` tipo por padrão) para que os eventos sejam publicados da maneira familiar para outras linguagens .net.

```fsharp
type MyBadType() =
    let myEv = new Event<int>()

    [<CLIEvent>]
    member this.MyEvent = myEv.Publish

type MyEventArgs(x: int) =
    inherit System.EventArgs()
    member this.X = x

    /// A type in a component designed for use from other .NET languages
type MyGoodType() =
    let myEv = new DelegateEvent<EventHandler<MyEventArgs>>()

    [<CLIEvent>]
    member this.MyEvent = myEv.Publish
```

#### <a name="expose-asynchronous-operations-as-methods-that-return-net-tasks"></a>Expor operações assíncronas como métodos que retornam tarefas .NET

As tarefas são usadas no .NET para representar Computações assíncronas ativas. As tarefas estão em geral menos composições que objetos F # `Async<T>` , já que representam tarefas "já em execução" e não podem ser compostas de maneiras que executam composição paralela ou que ocultam a propagação de sinais de cancelamento e outros parâmetros contextuais.

No entanto, apesar disso, os métodos que retornam tarefas são a representação padrão da programação assíncrona no .NET.

```fsharp
/// A type in a component designed for use from other .NET languages
type MyType() =

    let compute (x: int): Async<int> = async { ... }

    member this.ComputeAsync(x) = compute x |> Async.StartAsTask
```

Geralmente, você também desejará aceitar um token de cancelamento explícito:

```fsharp
/// A type in a component designed for use from other .NET languages
type MyType() =
    let compute(x: int): Async<int> = async { ... }
    member this.ComputeAsTask(x, cancellationToken) = Async.StartAsTask(compute x, cancellationToken)
```

#### <a name="use-net-delegate-types-instead-of-f-function-types"></a>Usar tipos de delegado do .NET em vez de tipos de função F #

Aqui "tipos de função F #" significam tipos de "seta" como `int -> int` .

Em vez disso:

```fsharp
member this.Transform(f: int->int) =
    ...
```

Faça o seguinte:

```fsharp
member this.Transform(f: Func<int,int>) =
    ...
```

O tipo de função F # aparece como `class FSharpFunc<T,U>` em outras linguagens .net e é menos adequado para recursos de linguagem e ferramentas que compreendem tipos delegados. Ao criar um método de ordem superior direcionado .NET Framework 3,5 ou superior, os `System.Func` `System.Action` delegados e são as APIs certas para publicar para permitir que os desenvolvedores do .net consumam essas APIs de maneira baixa-fricção. (Ao direcionar .NET Framework 2,0, os tipos delegados definidos pelo sistema são mais limitados; considere usar tipos delegados predefinidos, como `System.Converter<T,U>` ou definir um tipo de delegado específico.)

No lado do inverso, os delegados do .NET não são naturais para bibliotecas voltadas para o F # (consulte a próxima seção sobre bibliotecas em F #). Como resultado, uma estratégia de implementação comum ao desenvolver métodos de ordem superior para as bibliotecas do .NET da baunilha é criar toda a implementação usando tipos de função F # e, em seguida, criar a API pública usando delegados como uma fachada fina sobre a implementação real de F #.

#### <a name="use-the-trygetvalue-pattern-instead-of-returning-f-option-values-and-prefer-method-overloading-to-taking-f-option-values-as-arguments"></a>Use o padrão TryGetValue em vez de retornar valores de opção F # e prefira o sobrecarregamento de método para usar valores de opção F # como argumentos

Os padrões comuns de uso para o tipo de opção F # em APIs são melhor implementados nas APIs do .NET da baunilha usando técnicas de design padrão do .NET. Em vez de retornar um valor de opção de F #, considere usar o tipo de retorno bool mais um parâmetro out como no padrão "TryGetValue". E em vez de usar valores de opção F # como parâmetros, considere o uso de sobrecarga de método ou argumentos opcionais.

```fsharp
member this.ReturnOption() = Some 3

member this.ReturnBoolAndOut(outVal: byref<int>) =
    outVal <- 3
    true

member this.ParamOption(x: int, y: int option) =
    match y with
    | Some y2 -> x + y2
    | None -> x

member this.ParamOverload(x: int) = x

member this.ParamOverload(x: int, y: int) = x + y
```

#### <a name="use-the-net-collection-interface-types-ienumerablet-and-idictionarykeyvalue-for-parameters-and-return-values"></a>Usar os tipos de interface de coleção .NET IEnumerable \<T\> e IDictionary \<Key,Value\> para parâmetros e valores de retorno

Evite o uso de tipos de coleção concretos, como matrizes .NET `T[]` , tipos F # `list<T>` `Map<Key,Value>` e `Set<T>` tipos de coleção concretos .NET `Dictionary<Key,Value>` , como. As diretrizes de design de biblioteca do .NET têm bons conselhos sobre quando usar vários tipos de coleção como o `IEnumerable<T>` . Um pouco de uso de matrizes ( `T[]` ) é aceitável em algumas circunstâncias, no aterramento de desempenho. Observe especialmente que `seq<T>` é apenas o alias F # para `IEnumerable<T>` e, portanto, seq é geralmente um tipo apropriado para uma API .NET da baunilha.

Em vez de listas F #:

```fsharp
member this.PrintNames(names: string list) =
    ...
```

Usar sequências F #:

```fsharp
member this.PrintNames(names: seq<string>) =
    ...
```

#### <a name="use-the-unit-type-as-the-only-input-type-of-a-method-to-define-a-zero-argument-method-or-as-the-only-return-type-to-define-a-void-returning-method"></a>Use o tipo de unidade como o único tipo de entrada de um método para definir um método de argumento zero ou como o único tipo de retorno para definir um método de retorno nulo

Evite outros usos do tipo de unidade. Eles são bons:

```fsharp
✔ member this.NoArguments() = 3

✔ member this.ReturnVoid(x: int) = ()
```

Isso é inadequado:

```fsharp
member this.WrongUnit( x: unit, z: int) = ((), ())
```

#### <a name="check-for-null-values-on-vanilla-net-api-boundaries"></a>Verificar valores nulos nos limites da API .NET da baunilha

O código de implementação de F # tende a ter menos valores nulos, devido a padrões de design imutáveis e restrições no uso de literais nulos para tipos F #. Outras linguagens .NET geralmente usam NULL como um valor com muito mais frequência. Por isso, o código F # que está expondo uma API .NET da baunilha deve verificar os parâmetros de NULL no limite da API e impedir que esses valores fluam mais profundamente no código de implementação do F #. A `isNull` função ou o padrão correspondente no `null` padrão pode ser usado.

```fsharp
let checkNonNull argName (arg: obj) =
    match arg with
    | null -> nullArg argName
    | _ -> ()

let checkNonNull` argName (arg: obj) =
    if isNull arg then nullArg argName
    else ()
```

#### <a name="avoid-using-tuples-as-return-values"></a>Evite usar tuplas como valores de retorno

Em vez disso, prefira retornar um tipo nomeado contendo os dados agregados ou usar parâmetros de saída para retornar vários valores. Embora exista tuplas e tuplas de struct no .NET (incluindo suporte a linguagem C# para tuplas struct), elas geralmente não fornecem a API ideal e esperada para desenvolvedores .NET.

#### <a name="avoid-the-use-of-currying-of-parameters"></a>Evitar o uso de currying de parâmetros

Em vez disso, use as convenções de chamada .NET `Method(arg1,arg2,…,argN)` .

```fsharp
member this.TupledArguments(str, num) = String.replicate num str
```

Dica: se você estiver criando bibliotecas para uso a partir de qualquer linguagem .NET, não há nenhum substituto para realmente fazer um C# experimental e Visual Basic programação para garantir que suas bibliotecas "fiquem corretas" nessas linguagens. Você também pode usar ferramentas como o reflector do .NET e o pesquisador de objetos do Visual Studio para garantir que as bibliotecas e sua documentação apareçam conforme o esperado para os desenvolvedores.

## <a name="appendix"></a>Apêndice

### <a name="end-to-end-example-of-designing-f-code-for-use-by-other-net-languages"></a>Exemplo de ponta a ponta de criação de código F # para uso por outras linguagens .NET

Considere a seguinte classe:

```fsharp
open System

type Point1(angle,radius) =
    new() = Point1(angle=0.0, radius=0.0)
    member x.Angle = angle
    member x.Radius = radius
    member x.Stretch(l) = Point1(angle=x.Angle, radius=x.Radius * l)
    member x.Warp(f) = Point1(angle=f(x.Angle), radius=x.Radius)
    static member Circle(n) =
        [ for i in 1..n -> Point1(angle=2.0*Math.PI/float(n), radius=1.0) ]
```

O tipo F # inferido dessa classe é o seguinte:

```fsharp
type Point1 =
    new : unit -> Point1
    new : angle:double * radius:double -> Point1
    static member Circle : n:int -> Point1 list
    member Stretch : l:double -> Point1
    member Warp : f:(double -> double) -> Point1
    member Angle : double
    member Radius : double
```

Vamos dar uma olhada em como esse tipo F # aparece para um programador usando outra linguagem .NET. Por exemplo, a "assinatura" aproximada do C# é a seguinte:

```csharp
// C# signature for the unadjusted Point1 class
public class Point1
{
    public Point1();

    public Point1(double angle, double radius);

    public static Microsoft.FSharp.Collections.List<Point1> Circle(int count);

    public Point1 Stretch(double factor);

    public Point1 Warp(Microsoft.FSharp.Core.FastFunc<double,double> transform);

    public double Angle { get; }

    public double Radius { get; }
}
```

Há alguns pontos importantes a serem observados sobre como F # representa construções aqui. Por exemplo:

* Metadados como nomes de argumentos foram preservados.

* Os métodos F # que usam dois argumentos se tornam métodos C# que usam dois argumentos.

* Funções e listas se tornam referências a tipos correspondentes na biblioteca F #.

O código a seguir mostra como ajustar esse código para levar essas coisas em conta.

```fsharp
namespace SuperDuperFSharpLibrary.Types

type RadialPoint(angle:double, radius:double) =

    /// Return a point at the origin
    new() = RadialPoint(angle=0.0, radius=0.0)

    /// The angle to the point, from the x-axis
    member x.Angle = angle

    /// The distance to the point, from the origin
    member x.Radius = radius

    /// Return a new point, with radius multiplied by the given factor
    member x.Stretch(factor) =
        RadialPoint(angle=angle, radius=radius * factor)

    /// Return a new point, with angle transformed by the function
    member x.Warp(transform:Func<_,_>) =
        RadialPoint(angle=transform.Invoke angle, radius=radius)

    /// Return a sequence of points describing an approximate circle using
    /// the given count of points
    static member Circle(count) =
        seq { for i in 1..count ->
                RadialPoint(angle=2.0*Math.PI/float(count), radius=1.0) }
```

O tipo F # inferido do código é o seguinte:

```fsharp
type RadialPoint =
    new : unit -> RadialPoint
    new : angle:double * radius:double -> RadialPoint
    static member Circle : count:int -> seq<RadialPoint>
    member Stretch : factor:double -> RadialPoint
    member Warp : transform:System.Func<double,double> -> RadialPoint
    member Angle : double
    member Radius : double
```

A assinatura do C# agora é a seguinte:

```csharp
public class RadialPoint
{
    public RadialPoint();

    public RadialPoint(double angle, double radius);

    public static System.Collections.Generic.IEnumerable<RadialPoint> Circle(int count);

    public RadialPoint Stretch(double factor);

    public RadialPoint Warp(System.Func<double,double> transform);

    public double Angle { get; }

    public double Radius { get; }
}
```

As correções feitas para preparar esse tipo para uso como parte de uma biblioteca .NET da baunilha são as seguintes:

* Ajustou vários nomes: `Point1` ,, `n` `l` , e tornou-se `f` `RadialPoint` , `count` , `factor` e `transform` , respectivamente.

* Usou um tipo de retorno de `seq<RadialPoint>` em vez de `RadialPoint list` alterando uma construção de lista usando `[ ... ]` para uma construção de sequência usando `IEnumerable<RadialPoint>` .

* Usado o tipo de delegado do .NET `System.Func` em vez de um tipo de função F #.

Isso torna muito mais fácil consumir em código C#.
