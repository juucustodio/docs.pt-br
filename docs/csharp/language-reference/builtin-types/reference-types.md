---
title: Tipos de referência internos – Referência de C#
description: Saiba mais sobre os tipos de referência que têm palavras-chave do C# que você pode usar para declará-las.
ms.date: 06/25/2019
f1_keywords:
- object_CSharpKeyword
- object
- delegate_CSharpKeyword
- delegate
- dynamic_CSharpKeyword
- string
- string_CSharpKeyword
helpviewer_keywords:
- object keyword [C#]
- delegate keyword [C#]
- function pointers [C#]
- dynamic [C#]
- dynamic keyword [C#]
- strings [C#], reference
- '@ string literal'
- string literals [C#]
- string keyword [C#]
ms.openlocfilehash: c2c03f47babd9ccf87eb60d33b9d65d1a9c82e2e
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223510"
---
# <a name="built-in-reference-types-c-reference"></a>Tipos de referência internos (Referência de C#)

O C# tem um número de tipos de referência internos. Eles têm palavras-chave ou operadores que são sinônimos de um tipo na biblioteca do .NET.

## <a name="the-object-type"></a>O tipo de objeto

O tipo `object` é um alias de <xref:System.Object?displayProperty=nameWithType> no .NET. No sistema de tipos unificado do C#, todos os tipos, predefinidos e definidos pelo usuário, tipos de referência e tipos de valor, herdam direta ou indiretamente de <xref:System.Object?displayProperty=nameWithType>. Você pode atribuir valores de qualquer tipo a variáveis do tipo `object`. Qualquer variável `object` pode ser atribuída ao seu valor padrão usando o literal `null`. Quando uma variável de um tipo de valor é convertida para um objeto, ela é chamada de *boxed*. Quando uma variável do tipo `object` é convertida em um tipo Value, ele é considerado como *unboxed*. Para obter mais informações, consulte [Conversões boxing e unboxing](../../programming-guide/types/boxing-and-unboxing.md).

## <a name="the-string-type"></a>O tipo de cadeia de caracteres

O tipo `string` representa uma sequência de zero ou mais caracteres Unicode. `string` é um alias de <xref:System.String?displayProperty=nameWithType> no .NET.

Embora `string` seja um tipo de referência, os [operadores de igualdade `==` e `!=`](../operators/equality-operators.md#string-equality) são definidos para comparar os valores de objetos `string`, não referências. Isso torna o teste de igualdade de cadeia de caracteres mais intuitivo. Por exemplo:

```csharp-interactive
string a = "hello";
string b = "h";
// Append to contents of 'b'
b += "ello";
Console.WriteLine(a == b);
Console.WriteLine(object.ReferenceEquals(a, b));
```

Isso exibe "True" e, em seguida, "False" porque os conteúdos das cadeias de caracteres são equivalentes, mas `a` e `b` não fazem referência à mesma instância da cadeia de caracteres.

O [operador +](../operators/addition-operator.md#string-concatenation) concatena as cadeias de caracteres:

```csharp
string a = "good " + "morning";
```

Isso cria um objeto de cadeia de caracteres que contém “good morning”.

Cadeias de caracteres são *imutável* – o conteúdo de um objeto de cadeia de caracteres não pode ser alterado depois que o objeto é criado, embora a sintaxe faça com que pareça que você pode fazer isso. Por exemplo, quando você escreve esse código, o compilador, na verdade, cria um objeto de cadeia de caracteres para manter a nova sequência de caracteres e esse novo objeto é atribuído a `b`. A memória que tiver sido alocada para `b` (quando ela continha a cadeia de caracteres "h") será elegível para a coleta de lixo.

```csharp
string b = "h";
b += "ello";
```

O `[]` [operador](../operators/member-access-operators.md#indexer-operator-) pode ser usado para acesso somente leitura a caracteres individuais de uma cadeia de caracteres. Os valores de índice válidos começam em `0` e devem ser menores que o comprimento da cadeia de caracteres:

```csharp
string str = "test";
char x = str[2];  // x = 's';
```

De maneira semelhante, o `[]` operador também pode ser usado para iterar em cada caractere em uma cadeia de caracteres:

```csharp-interactive
string str = "test";

for (int i = 0; i < str.Length; i++)
{
  Console.Write(str[i] + " ");
}
// Output: t e s t
```

Literais de cadeia de caracteres são do tipo `string` e podem ser escritos de duas formas, entre aspas e `@`. Os literais de cadeia de caracteres entre aspas são colocados entre aspas duplas ("):

```csharp
"good morning"  // a string literal
```

Os literais de cadeia de caracteres podem conter qualquer literal de caractere. Sequências de escape são incluídas. O exemplo a seguir usa a sequência de escape `\\` de barra invertida, `\u0066` para a letra f e `\n` para a nova linha.

```csharp-interactive
string a = "\\\u0066\n F";
Console.WriteLine(a);
// Output:
// \f
//  F
```

> [!NOTE]
> O código de escape `\udddd` (em que `dddd` é um número de quatro dígitos) representa o caractere Unicode U+`dddd`. Os códigos de escape Unicode de oito dígitos também são reconhecidos: `\Udddddddd`.

Os [literais de cadeia de caracteres textuais](../tokens/verbatim.md) começam com `@` e também são colocados entre aspas duplas. Por exemplo:

```csharp
@"good morning"  // a string literal
```

A vantagem das cadeias de caracteres textuais é que as sequências de escape *não* são processadas, o que torna mais fácil escrever, por exemplo, um nome de arquivo totalmente qualificado do Windows:

```csharp
@"c:\Docs\Source\a.txt"  // rather than "c:\\Docs\\Source\\a.txt"
```

Para incluir aspas duplas em uma cadeia de caracteres @-quoted, dobre-a:

```csharp
@"""Ahoy!"" cried the captain." // "Ahoy!" cried the captain.
```

## <a name="the-delegate-type"></a>O tipo de delegado

A declaração de um tipo de delegado é semelhante a uma assinatura de método. Ela tem um valor retornado e parâmetros de qualquer tipo:

```csharp
public delegate void MessageDelegate(string message);
public delegate int AnotherDelegate(MyType m, long num);
```

No .NET, os tipos `System.Action` e `System.Func` fornecem definições genéricas para muitos delegados comuns. Você provavelmente não precisa definir novos tipos de delegado personalizado. Em vez disso, é possível criar instâncias dos tipos genéricos fornecidos.

Um `delegate` é um tipo de referência que pode ser usado para encapsular um método nomeado ou anônimo. Representantes são semelhantes a ponteiros de função em C++. No entanto, os representantes são fortemente tipados e seguros. Para aplicativos de representantes, consulte [Representantes](../../programming-guide/delegates/index.md) e [Representantes genéricos](../../programming-guide/generics/generic-delegates.md). Os representantes são a base dos [Eventos](../../programming-guide/events/index.md). Um delegado pode ser instanciado associando-o a um método nomeado ou anônimo.

O delegado deve ser instanciado com um método ou expressão lambda que tenha um tipo de retorno compatível e parâmetros de entrada. Para obter mais informações sobre o grau de variação permitido na assinatura do método, consulte [Variação em representantes](../../programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md). Para uso com métodos anônimos, o delegado e o código a ser associado a ele são declarados juntos.

## <a name="the-dynamic-type"></a>O tipo dinâmico

O tipo `dynamic` indica que o uso de variável e as referências aos seus membros ignoram a verificação de tipo de tempo de compilação. Em vez disso, essas operações são resolvidas em tempo de execução. O tipo `dynamic` simplifica o acesso a APIs COM, como as APIs de Automação do Office e também às APIs dinâmicas, como bibliotecas do IronPython e ao DOM (Modelo de Objeto do Documento) HTML.

O tipo `dynamic` se comporta como o tipo `object` na maioria das circunstâncias. Em particular, qualquer expressão não nula pode ser convertida no tipo `dynamic`. O tipo `dynamic` é diferente de `object` nas operações que contêm expressões do tipo `dynamic` não resolvidas ou com tipo verificado pelo compilador. O compilador junta as informações sobre a operação em pacotes e, posteriormente, essas informações são usadas para avaliar a operação em tempo de execução. Como parte do processo, as variáveis do tipo `dynamic` são compiladas em variáveis do tipo `object`. Portanto, o tipo `dynamic` existe somente em tempo de compilação e não em tempo de execução.

O exemplo a seguir compara uma variável do tipo `dynamic` a uma variável do tipo `object`. Para verificar o tipo de cada variável no tempo de compilação, coloque o ponteiro do mouse sobre `dyn` ou `obj` nas instruções `WriteLine`. Copie o seguinte código para um editor em que o IntelliSense está disponível. O IntelliSense mostra **dinâmico** para `dyn` e **objeto** para `obj`.

[!code-csharp[csrefKeywordsTypes#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/dynamic1.cs#21)]

As instruções <xref:System.Console.WriteLine%2A> exibem os tipos de tempo de execução de `dyn` e `obj`. Nesse ponto, ambos têm o mesmo tipo, inteiro. A seguinte saída é produzida:

```console
System.Int32
System.Int32
```

Para ver a diferença entre `dyn` e `obj` em tempo de compilação, adicione as duas linhas a seguir entre as declarações e as instruções `WriteLine` no exemplo anterior.

```csharp
dyn = dyn + 3;
obj = obj + 3;
```

 Um erro de compilador será relatado em virtude da tentativa de adição de um inteiro e um objeto à expressão `obj + 3`. No entanto, nenhum erro será relatado para `dyn + 3`. A expressão contém `dyn` não é verificada em tempo de compilação, pois o tipo de `dyn` é `dynamic`.

O exemplo a seguir usa `dynamic` em várias declarações. O método `Main` também compara a verificação de tipo em tempo de compilação com a verificação de tipo em tempo de execução.

[!code-csharp[csrefKeywordsTypes#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/dynamic2.cs#25)]

### <a name="see-also"></a>Consulte também

- [Referência do C#](../index.md)
- [Palavras-chave do C#](../keywords/index.md)
- [Eventos](../../programming-guide/events/index.md)
- [Usando o tipo dynamic](../../programming-guide/types/using-type-dynamic.md)
- [Práticas recomendadas para usar cadeias de caracteres](../../../standard/base-types/best-practices-strings.md)
- [Operações básicas de cadeia de caracteres](../../../standard/base-types/basic-string-operations.md)
- [Criar novas cadeias de caracteres](../../../standard/base-types/creating-new.md)
- [Operadores cast e teste de tipo](../operators/type-testing-and-cast.md)
- [Como converter com segurança usando correspondência de padrões e os operadores as e is](../../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md)
- [Passo a passo: Criando e usando objetos dinâmicos](../../programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)
- <xref:System.Object?displayProperty=nameWithType>
- <xref:System.String?displayProperty=nameWithType>
- <xref:System.Dynamic.DynamicObject?displayProperty=nameWithType>
