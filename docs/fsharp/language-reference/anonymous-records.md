---
title: Registros Anônimos
description: Saiba como usar a construção e o uso de registros anônimos, um recurso de linguagem que ajuda na manipulação de dados.
ms.date: 06/12/2019
ms.openlocfilehash: 13950048f02ab74362f8174725f5f8615d9d7654
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739809"
---
# <a name="anonymous-records"></a>Registros Anônimos

Registros anônimos são agregações simples de valores nomeados que não precisam ser declarados antes do uso. Você pode declará-los como structs ou tipos de referência. Eles são tipos de referência por padrão.

## <a name="syntax"></a>Sintaxe

Os exemplos a seguir demonstram a sintaxe de registro anônimo. Os itens delimitados como `[item]` são opcionais.

```fsharp
// Construct an anonymous record
let value-name = [struct] {| Label1: Type1; Label2: Type2; ...|}

// Use an anonymous record as a type parameter
let value-name = Type-Name<[struct] {| Label1: Type1; Label2: Type2; ...|}>

// Define a parameter with an anonymous record as input
let function-name (arg-name: [struct] {| Label1: Type1; Label2: Type2; ...|}) ...
```

## <a name="basic-usage"></a>Uso básico

Os registros anônimos são mais bem considerados como tipos de registro F # que não precisam ser declarados antes da instanciação.

Por exemplo, aqui, como você pode interagir com uma função que produz um registro anônimo:

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

O exemplo a seguir expande o anterior com uma `printCircleStats` função que usa um registro anônimo como entrada:

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let printCircleStats r (stats: {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

Chamar `printCircleStats` com qualquer tipo de registro anônimo que não tem a mesma "forma", pois o tipo de entrada falhará na compilação:

```fsharp
printCircleStats r {| Diameter = 2.0; Area = 4.0; MyCircumference = 12.566371 |}
// Two anonymous record types have mismatched sets of field names
// '["Area"; "Circumference"; "Diameter"]' and '["Area"; "Diameter"; "MyCircumference"]'
```

## <a name="struct-anonymous-records"></a>Registros anônimos de struct

Os registros anônimos também podem ser definidos como struct com a `struct` palavra-chave Optional. O exemplo a seguir aumenta o anterior, produzindo e consumindo um registro anônimo de struct:

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    // Note that the keyword comes before the '{| |}' brace pair
    struct {| Area = a; Circumference = c; Diameter = d |}

// the 'struct' keyword also comes before the '{| |}' brace pair when declaring the parameter type
let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

### <a name="structness-inference"></a>Inferência de estrutura

Os registros anônimos de struct também permitem a "inferência de estruturação", em que não é necessário especificar a `struct` palavra-chave no site de chamada. Neste exemplo, você elide a `struct` palavra-chave ao chamar `printCircleStats` :

```fsharp

let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

printCircleStats r {| Area = 4.0; Circumference = 12.6; Diameter = 12.6 |}
```

O padrão inverso-especificar `struct` quando o tipo de entrada não é um registro anônimo de struct-falhará na compilação.

## <a name="embedding-anonymous-records-within-other-types"></a>Inserindo registros anônimos em outros tipos

É útil declarar [uniões discriminadas](discriminated-unions.md) cujos casos são registros. Mas se os dados nos registros forem do mesmo tipo que a união discriminada, você deverá definir todos os tipos como mutuamente recursivos. O uso de registros anônimos evita essa restrição. O que vem a seguir é um tipo de exemplo e função que o padrão corresponde a ele:

```fsharp
type FullName = { FirstName: string; LastName: string }

// Note that using a named record for Manager and Executive would require mutually recursive definitions.
type Employee =
    | Engineer of FullName
    | Manager of {| Name: FullName; Reports: Employee list |}
    | Executive of {| Name: FullName; Reports: Employee list; Assistant: Employee |}

let getFirstName e =
    match e with
    | Engineer fullName -> fullName.FirstName
    | Manager m -> m.Name.FirstName
    | Executive ex -> ex.Name.FirstName
```

## <a name="copy-and-update-expressions"></a>Copiar e atualizar expressões

Os registros anônimos dão suporte à construção com [expressões de cópia e atualização](copy-and-update-record-expressions.md). Por exemplo, veja como você pode construir uma nova instância de um registro anônimo que copia os dados de um existente:

```fsharp
let data = {| X = 1; Y = 2 |}
let data' = {| data with Y = 3 |}
```

No entanto, ao contrário dos registros nomeados, os registros anônimos permitem que você construa formulários totalmente diferentes com expressões de cópia e atualização. O exemplo a seguir usa o mesmo registro anônimo do exemplo anterior e o expande para um novo registro anônimo:

```fsharp
let data = {| X = 1; Y = 2 |}
let expandedData = {| data with Z = 3 |} // Gives {| X=1; Y=2; Z=3 |}
```

Também é possível construir registros anônimos de instâncias de registros nomeados:

```fsharp
type R = { X: int }
let data = { X = 1 }
let data' = {| data with Y = 2 |} // Gives {| X=1; Y=2 |}
```

Você também pode copiar dados de e para registros anônimos de referência e de struct:

```fsharp
// Copy data from a reference record into a struct anonymous record
type R1 = { X: int }
let r1 = { X = 1 }

let data1 = struct {| r1 with Y = 1 |}

// Copy data from a struct record into a reference anonymous record
[<Struct>]
type R2 = { X: int }
let r2 = { X = 1 }

let data2 = {| r1 with Y = 1 |}

// Copy the reference anonymous record data into a struct anonymous record
let data3 = struct {| data2 with Z = r2.X |}
```

## <a name="properties-of-anonymous-records"></a>Propriedades de registros anônimos

Os registros anônimos têm uma série de características essenciais para compreender totalmente como elas podem ser usadas.

### <a name="anonymous-records-are-nominal"></a>Registros anônimos são nominal

Os registros anônimos são [tipos nominais](https://en.wikipedia.org/wiki/Nominal_type_system). Eles são mais bem pensados como tipos de [registros](records.md) nomeados (que também são nominais) que não exigem uma declaração inicial.

Considere o exemplo a seguir com duas declarações de registro anônimos:

```fsharp
let x = {| X = 1 |}
let y = {| Y = 1 |}
```

Os `x` `y` valores e têm tipos diferentes e não são compatíveis um com o outro. Elas não são intrínsecas e não são comparáveis. Para ilustrar isso, considere um registro nomeado equivalente:

```fsharp
type X = { X: int }
type Y = { Y: int }

let x = { X = 1 }
let y = { Y = 1 }
```

Não há nada inerentemente diferente sobre registros anônimos quando comparado com seus equivalentes de registro nomeados quando se trata da equivalência ou da comparação de tipo.

### <a name="anonymous-records-use-structural-equality-and-comparison"></a>Registros anônimos usam igualdade e comparação estrutural

Assim como os tipos de registro, os registros anônimos são estruturais e comparáveis. Isso só será verdadeiro se todos os tipos constituintes suportarem igualdade e comparação, como com os tipos de registro. Para dar suporte a igualdade ou comparação, dois registros anônimos devem ter a mesma "forma".

```fsharp
{| a = 1+1 |} = {| a = 2 |} // true
{| a = 1+1 |} > {| a = 1 |} // true

// error FS0001: Two anonymous record types have mismatched sets of field names '["a"]' and '["a"; "b"]'
{| a = 1 + 1 |} = {| a = 2;  b = 1|}
```

### <a name="anonymous-records-are-serializable"></a>Os registros anônimos são serializáveis

Você pode serializar registros anônimos assim como é possível com registros nomeados. Aqui está um exemplo usando [Newtonsoft.Jsem](https://www.nuget.org/packages/Newtonsoft.Json/):

```fsharp
open Newtonsoft.Json

let phillip' = {| name="Phillip"; age=28 |}
let philStr = JsonConvert.SerializeObject(phillip')

let phillip = JsonConvert.DeserializeObject<{|name: string; age: int|}>(philStr)
printfn $"Name: {phillip.name} Age: %d{phillip.age}"
```

Os registros anônimos são úteis para o envio de dados leves por uma rede sem a necessidade de definir um domínio para os tipos serializados/desserializados antecipadamente.

### <a name="anonymous-records-interoperate-with-c-anonymous-types"></a>Registros anônimos interoperam com tipos anônimos do C#

É possível usar uma API do .NET que exija o uso de [tipos anônimos em C#](../../csharp/programming-guide/classes-and-structs/anonymous-types.md). Os tipos anônimos do C# são triviais para interoperar com o usando registros anônimos. O exemplo a seguir mostra como usar registros anônimos para chamar uma sobrecarga [LINQ](../../csharp/programming-guide/concepts/linq/index.md) que requer um tipo anônimo:

```fsharp
open System.Linq

let names = [ "Ana"; "Felipe"; "Emilia"]
let nameGrouping = names.Select(fun n -> {| Name = n; FirstLetter = n.[0] |})
for ng in nameGrouping do
    printfn $"{ng.Name} has first letter {ng.FirstLetter}"
```

Há uma infinidade de outras APIs usadas em todo o .NET que exigem o uso de passar um tipo anônimo. Os registros anônimos são sua ferramenta para trabalhar com eles.

## <a name="limitations"></a>Limitações

Os registros anônimos têm algumas restrições em seu uso. Algumas são inerentes ao seu design, mas outras são receptivos para alterar.

### <a name="limitations-with-pattern-matching"></a>Limitações com correspondência de padrões

Os registros anônimos não dão suporte à correspondência de padrões, ao contrário dos registros nomeados. Há três motivos:

1. Um padrão teria que considerar cada campo de um registro anônimo, diferentemente dos tipos de registro nomeados. Isso ocorre porque os registros anônimos não dão suporte à subdigitação estrutural – são tipos nominais.
2. Por causa de (1), não há capacidade de ter padrões adicionais em uma expressão de correspondência de padrões, pois cada padrão distinto implicaria em um tipo de registro anônimo diferente.
3. Por causa do (3), qualquer padrão de registro anônimo seria mais detalhado do que o uso da notação "ponto".

Há uma sugestão de linguagem aberta para [permitir a correspondência de padrões em contextos limitados](https://github.com/fsharp/fslang-suggestions/issues/713).

### <a name="limitations-with-mutability"></a>Limitações com a imutabilidade

No momento, não é possível definir um registro anônimo com `mutable` dados. Há uma [sugestão de linguagem aberta](https://github.com/fsharp/fslang-suggestions/issues/732) para permitir dados mutáveis.

### <a name="limitations-with-struct-anonymous-records"></a>Limitações com registros anônimos de struct

Não é possível declarar registros anônimos de struct como `IsByRefLike` ou `IsReadOnly` . Há uma [sugestão de linguagem aberta](https://github.com/fsharp/fslang-suggestions/issues/712) para `IsByRefLike` registros de e `IsReadOnly` anônimos.
