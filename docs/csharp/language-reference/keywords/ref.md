---
description: Palavra-chave ref – Referência de C#
title: Palavra-chave ref – Referência de C#
ms.date: 04/21/2020
f1_keywords:
- ref_CSharpKeyword
- ref
helpviewer_keywords:
- parameters [C#], ref
- ref keyword [C#]
ms.openlocfilehash: d2855738c723ba6d2437257793f18349b18629dc
ms.sourcegitcommit: eb7e87496f42361b1da98562dd75b516c9d58bbc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91877581"
---
# <a name="ref-c-reference"></a>ref (Referência de C#)

A palavra-chave `ref` indica um valor que é passado por referência. Ela é usada em quatro contextos diferentes:

- Em uma assinatura de método e em uma chamada de método, para passar um argumento a um método por referência. Para obter mais informações, veja [Passar um argumento por referência](#passing-an-argument-by-reference).
- Em uma assinatura de método para retornar um valor para o chamador por referência. Para obter mais informações, consulte [Reference return values](#reference-return-values) (Valores retornados de referência).
- Em um corpo de membro, para indicar que um valor retornado por referência é armazenado localmente como uma referência que o chamador pretende modificar ou, em geral, uma variável local acessa outro valor por referência. Para obter mais informações, veja [Locais de referência](#ref-locals).
- Em uma declaração `struct` para declarar um `ref struct` ou um `readonly ref struct`. Para obter mais informações, consulte a seção [ `ref` struct](../builtin-types/struct.md#ref-struct) do artigo [tipos de estrutura](../builtin-types/struct.md) .

## <a name="passing-an-argument-by-reference"></a>Passando um argumento por referência

Quando usado na lista de parâmetros do método, a palavra-chave `ref` indica que um argumento é passado por referência, não por valor. A palavra-chave `ref` torna o parâmetro formal um alias para o argumento, que deve ser uma variável. Em outras palavras, qualquer operação no parâmetro é feita no argumento. Por exemplo, se o chamador passar uma expressão de variável local ou uma expressão de acesso de elemento de matriz, e o método chamado substituir o objeto ao qual o parâmetro ref se refere, a variável local do chamador ou o elemento de matriz agora se referirá ao novo objeto quando o método retornar.

> [!NOTE]
> Não confunda o conceito de passar por referência com o conceito de tipos de referência. Os dois conceitos não são iguais. Um parâmetro de método pode ser modificado por `ref`, independentemente de ele ser um tipo de valor ou um tipo de referência. Não há nenhuma conversão boxing de um tipo de valor quando ele é passado por referência.  

Para usar um parâmetro `ref`, a definição do método e o método de chamada devem usar explicitamente a palavra-chave `ref`, como mostrado no exemplo a seguir.  

[!code-csharp-interactive[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#1)]

Um argumento passado para um parâmetro `ref` ou `in` precisa ser inicializado antes de ser passado. Isso é diferente dos parâmetros [out](out-parameter-modifier.md), cujos argumentos não precisam ser inicializados explicitamente antes de serem passados.

Os membros de uma classe não podem ter assinaturas que se diferem somente por `ref`, `in` ou `out`. Ocorrerá um erro de compilador se a única diferença entre os dois membros de um tipo for que um deles tem um parâmetro `ref` e o outro tem um parâmetro `out` ou `in`. O código a seguir, por exemplo, não é compilado.  

```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```

No entanto, os métodos podem ser sobrecarregados quando um método tem um parâmetro `ref`, `in` ou `out` e o outro tem um parâmetro de valor, conforme é mostrado no exemplo a seguir.
  
[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#2)]
  
 Em outras situações que exigem correspondência de assinatura, como ocultar ou substituir, `in`, `ref` e `out` fazem parte da assinatura e não são correspondentes.  
  
 Propriedades não são variáveis. Elas são métodos e não podem ser passadas para parâmetros `ref`.  
  
 Não é possível usar as palavras-chave `ref`, `in` e `out` para os seguintes tipos de métodos:  
  
- Métodos assíncronos, que você define usando o modificador [async](async.md).  
- Métodos de iterador, que incluem uma instrução [yield return](yield.md) ou `yield break`.

Além disso, os [métodos de extensão](../../programming-guide/classes-and-structs/extension-methods.md) têm as seguintes restrições:

- A `out` palavra-chave não pode ser usada no primeiro argumento de um método de extensão.
- A `ref` palavra-chave não pode ser usada no primeiro argumento de um método de extensão quando o argumento não é um struct ou um tipo genérico não restrito a ser um struct.
- A `in` palavra-chave não pode ser usada, a menos que o primeiro argumento seja um struct. A `in` palavra-chave não pode ser usada em nenhum tipo genérico, mesmo quando restrita a um struct.

## <a name="passing-an-argument-by-reference-an-example"></a>Passando um argumento por referência: um exemplo

Os exemplos anteriores passam tipos de valor por referência. Você também pode usar a palavra-chave `ref` para passar tipos de referência por referência. Passar um tipo de referência por referência permite que o método chamado substitua o objeto ao qual se refere o parâmetro de referência no chamador. O local de armazenamento do objeto é passado para o método como o valor do parâmetro de referência. Se você alterar o valor no local de armazenamento do parâmetro (para apontar para um novo objeto), irá alterar também o local de armazenamento ao qual se refere o chamador. O exemplo a seguir passa uma instância de um tipo de referência como um parâmetro `ref`.
  
[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#3)]

Para obter mais informações sobre como passar tipos de referência por valor e por referência, consulte [Passando parâmetros de tipo de referência](../../programming-guide/classes-and-structs/passing-reference-type-parameters.md).
  
## <a name="reference-return-values"></a>Valores retornados por referência

Valores retornados por referência (ou ref returns) são valores que um método retorna por referência para o chamador. Ou seja, o chamador pode modificar o valor retornado por um método e essa alteração é refletida no estado do objeto no método de chamada.

Um valor retornado por referência é definido usando a palavra-chave `ref`:

- Na assinatura do método. Por exemplo, a assinatura de método a seguir indica que o método `GetCurrentPrice` retorna um valor <xref:System.Decimal> por referência.

```csharp
public ref decimal GetCurrentPrice()
```

- Entre o token `return` e a variável retornada em uma instrução `return` no método. Por exemplo:

```csharp
return ref DecimalArray[0];
```

Para que o chamador modifique o estado do objeto, o valor retornado de referência deve ser armazenado em uma variável que é definida explicitamente como um [ref local](#ref-locals).

Aqui está um exemplo de retorno de referência mais completo, mostrando a assinatura do método e o corpo do método.

[!code-csharp[FindReturningRef](~/samples/snippets/csharp/new-in-7/MatrixSearch.cs#FindReturningRef "Find returning by reference")]

O método chamado também poderá declarar o valor retornado como `ref readonly` para retornar o valor por referência e, em seguida, impor que o código de chamada não possa modificar o valor retornado. O método de chamada pode evitar copiar o valor retornado armazenando o valor em uma variável [ref ReadOnly](#ref-readonly-locals) local.

Para obter um exemplo, consulte [um exemplo de referências de ref e ref local](#a-ref-returns-and-ref-locals-example).

## <a name="ref-locals"></a>Ref locals

Uma variável de ref local é usada para fazer referência a valores retornados usando `return ref`. Uma variável local ref não pode ser inicializada para um valor retornado que não seja ref. Em outras palavras, o lado direito da inicialização deve ser uma referência. Todas as modificações ao valor do ref local são refletidas no estado do objeto cujo método retornou o valor por referência.

Você define um ref local usando a palavra-chave `ref` antes da declaração de variável, bem como imediatamente antes da chamada para o método que retorna o valor por referência.

Por exemplo, a instrução a seguir define um valor de ref local que é retornado por um método chamado `GetEstimatedValue`:

```csharp
ref decimal estValue = ref Building.GetEstimatedValue();
```

Você pode acessar um valor por referência da mesma maneira. Em alguns casos, acessar um valor por referência aumenta o desempenho, evitando uma operação de cópia potencialmente dispendiosa. Por exemplo, a instrução a seguir mostra como é possível definir um valor de local de ref que é usado para fazer referência a um valor.

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct;
```

Em ambos os exemplos `ref` , a palavra-chave deve ser usada em ambos os locais ou o compilador gera o erro CS8172, "não é possível inicializar uma variável por referência com um valor".

A partir do C# 7.3, a variável de iteração da instrução `foreach` pode ser ref local ou a variável local ref readonly. Para saber mais, confira o artigo [Instrução foreach](foreach-in.md).

Além de começar com o C# 7,3, você pode reatribuir uma variável local ref local ou ref ReadOnly com o [operador ref Assignment](../operators/assignment-operator.md#ref-assignment-operator).

## <a name="ref-readonly-locals"></a>Locais somente leitura de referência

Um local ref readonly é usado para fazer referência a valores retornados pelo método ou propriedade que tem `ref readonly` na sua assinatura e usa `return ref`. Uma variável `ref readonly` combina as propriedades de uma variável `ref` local com uma variável `readonly`: é um alias para o armazenamento ao qual está atribuído e não pode ser modificado.

## <a name="a-ref-returns-and-ref-locals-example"></a>Um exemplo de ref returns e ref locals

O exemplo a seguir define uma classe `Book` que tem dois campos <xref:System.String>, `Title` e `Author`. Ele também define uma classe `BookCollection` que inclui uma matriz privada de objetos `Book`. Objetos de catálogo individuais são retornados por referência chamando o respectivo método `GetBookByTitle`.

[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#4)]

Quando o chamador armazena o valor retornado pelo método `GetBookByTitle` como um ref local, as alterações que o chamador faz ao valor retornado são refletidas no objeto `BookCollection`, conforme mostra o exemplo a seguir.

[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#5)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Confira também

- [Escrever código eficiente seguro](../../write-safe-efficient-code.md)
- [Ref returns e ref locals](../../programming-guide/classes-and-structs/ref-returns.md)
- [Expressão condicional ref](../operators/conditional-operator.md#conditional-ref-expression)
- [Passando parâmetros](../../programming-guide/classes-and-structs/passing-parameters.md)
- [Parâmetros de método](method-parameters.md)
- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Palavras-chave do C#](index.md)
