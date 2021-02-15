---
title: Sintaxe detalhada
description: 'Aprenda a diferença entre a sintaxe detalhada e leve na linguagem de programação F #.'
ms.date: 05/16/2016
ms.openlocfilehash: 4e1725b58c8cb67c074ba12fd4ca25ce0c000a1e
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97595171"
---
# <a name="verbose-syntax"></a>Sintaxe detalhada

Há duas formas de sintaxe disponíveis para muitas construções na linguagem F #: *sintaxe detalhada* e *sintaxe leve*. A sintaxe detalhada não é normalmente usada, mas tem a vantagem de ser menos sensível ao recuo. A sintaxe leve é mais curta e usa recuo para sinalizar o início e o fim de construções, em vez de palavras-chave adicionais como `begin` , `end` , `in` e assim por diante. A sintaxe padrão é a sintaxe leve. Este tópico descreve a sintaxe para construções F # quando a sintaxe leve não está habilitada. A sintaxe detalhada é sempre habilitada, portanto, mesmo que você habilite a sintaxe leve, você ainda pode usar a sintaxe detalhada para algumas construções. Você pode desabilitar a sintaxe leve usando a `#light "off"` diretiva.

## <a name="table-of-constructs"></a>Tabela de construções

A tabela a seguir mostra a sintaxe leve e detalhada para construções de linguagem F # em contextos em que há uma diferença entre as duas formas. Nesta tabela, colchetes angulares ( &lt; &gt; ) incluem elementos de sintaxe fornecidos pelo usuário. Consulte a documentação de cada construção de linguagem para obter informações mais detalhadas sobre a sintaxe usada dentro dessas construções.

<table>
<tr>
<th>Construção de linguagem</th>
<th>Sintaxe leve</th>
<th>Sintaxe detalhada</th>
</tr>
<tr>
<td>
expressões compostas
</td>
<td>

```fsharp
<expression1>
<expression2>
```

</td><td>

```fsharp
<expression1>; <expression2>
```

</td>
</tr>
<tr><td>

associações aninhadas `let`

</td><td>

```fsharp
let f x =
    let a = 1
    let b = 2
    x + a + b
```

</td><td>

```fsharp
let f x =
    let a = 1 in
    let b = 2 in
    x + a + b
```

</td>
</tr>
<tr><td>
bloco de código
</td><td>

```fsharp
(
    <expression1>
    <expression2>
)
```

</td><td>

```fsharp
begin
    <expression1>;
    <expression2>;
end
```

</td>
</tr>
<tr><td>
`for...do`
</td><td>

```fsharp
for counter = start to finish do
    ...
```

</td><td>

```fsharp
for counter = start to finish do
    ...
done
```

</td>
</tr>
<tr><td>
`while...do`
</td><td>

```fsharp
while <condition> do
    ...
```

</td><td>

```fsharp
while <condition> do
    ...
done
```

</td>
</tr>
<tr><td>
`for...in`
</td><td>

```fsharp
for var in start .. finish do
    ...
```

</td><td>

```fsharp
for var in start .. finish do
    ...
done
```

</td>
</tr>
<tr><td>
`do`
</td><td>

```fsharp
do
    ...
```

</td><td>

```fsharp
do
    ...
in
```

</td>
</tr>
<tr><td>registro
</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    <value-or-member-definitions>
```

</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>classe
</td><td>

```fsharp
type <class-name>(<params>) =
    ...
```

</td><td>

```fsharp
type <class-name>(<params>) =
    class
        ...
    end
```

</td>
</tr>
<tr><td>estrutura</td><td>

```fsharp
[<StructAttribute>]
type <structure-name> =
    ...
```

</td><td>

```fsharp
type <structure-name> =
    struct
        ...
    end
```

</td>
</tr>
<tr><td>união discriminada</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    <value-or-member definitions>
```

</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>interface</td><td>

```fsharp
type <interface-name> =
    ...
```

</td><td>

```fsharp
type <interface-name> =
    interface
        ...
    end
```

</td>
</tr>
<tr><td>expressão de objeto</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
        <interface-implementations>
}
```

</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
    end
    <interface-implementations>
}
```

</td>
</tr>
<tr><td>implementação de interface</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>extensão de tipo</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>module</td><td>

```fsharp
module <module-name> =
    ...
```

</td><td>

```fsharp
module <module-name> =
    begin
        ...
    end
```

</td>
</tr>
</table>

## <a name="see-also"></a>Confira também

- [Referência de linguagem F #](index.md)
- [Diretivas de compilador](compiler-directives.md)
- [Diretrizes de Formatação de Código](../style-guide/formatting.md)
