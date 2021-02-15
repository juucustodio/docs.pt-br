---
title: Tipos de referência anuláveis – referência C#
description: Saiba mais sobre os tipos de referência nulos do C# e como usá-los
ms.date: 04/06/2020
ms.openlocfilehash: d961af9ba3b4776e6b4ec3eeea5392fb0d0394ce
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94822419"
---
# <a name="nullable-reference-types-c-reference"></a>Tipos de referência anuláveis (referência C#)

> [!NOTE]
> Este artigo aborda os tipos de referência anuláveis. Você também pode declarar [tipos de valor anulável](nullable-value-types.md).

Os tipos de referência anuláveis estão disponíveis a partir do C# 8,0, no código que aceitou um *contexto de reconhecimento anulável*. Tipos de referência anuláveis, os avisos de análise estática nula e o [operador NULL-tolerante](../operators/null-forgiving.md) são recursos de linguagem opcionais. Todos estão desativados por padrão. Um *contexto anulável* é controlado no nível do projeto usando as configurações de compilação ou no código usando pragmas.

 Em um contexto de reconhecimento anulável:

- Uma variável de um tipo de referência `T` deve ser inicializada com não nulo e talvez nunca seja atribuído um valor que possa ser `null` .
- Uma variável de um tipo de referência `T?` pode ser inicializada `null` ou atribuída `null` , mas precisa ser verificada `null` antes de remover a referência.
- Uma variável `m` do tipo `T?` é considerada como não nula quando você aplica o operador NULL-tolerante, como em `m!` .

As distinções entre um tipo de referência não anulável `T` e um tipo de referência Anulável `T?` são impostas pela interpretação do compilador das regras anteriores. Uma variável do tipo `T` e uma variável do tipo `T?` são representadas pelo mesmo tipo .net. O exemplo a seguir declara uma cadeia de caracteres não anulável e uma cadeia de caracteres anulável e, em seguida, usa o operador NULL-tolerante para atribuir um valor a uma cadeia de caracteres não anulável:

:::code language="csharp" source="snippets/shared/NullableReferenceTypes.cs" id="SnippetCoreSyntax":::

As variáveis `notNull` e `nullable` são representadas pelo <xref:System.String> tipo. Como os tipos não anuláveis e anuláveis são armazenados como o mesmo tipo, há vários locais em que o uso de um tipo de referência anulável não é permitido. Em geral, um tipo de referência anulável não pode ser usado como uma classe base ou uma interface implementada. Um tipo de referência anulável não pode ser usado em qualquer criação de objeto ou expressão de teste de tipo. Um tipo de referência anulável não pode ser o tipo de uma expressão de acesso de membro. Os exemplos a seguir mostram essas construções:

```csharp
public MyClass : System.Object? // not allowed
{
}

var nullEmpty = System.String?.Empty; // Not allowed
var maybeObject = new object?(); // Not allowed
try
{
    if (thing is string? nullableString) // not allowed
        Console.WriteLine(nullableString);
} catch (Exception? e) // Not Allowed
{
    Console.WriteLine("error");
}
```

## <a name="nullable-references-and-static-analysis"></a>Referências anuláveis e análise estática

Os exemplos na seção anterior ilustram a natureza dos tipos de referência anuláveis. Tipos de referência anuláveis não são novos tipos de classe, mas sim anotações em tipos de referência existentes. O compilador usa essas anotações para ajudá-lo a encontrar possíveis erros de referência nula em seu código. Não há nenhuma diferença de tempo de execução entre um tipo de referência não anulável e um tipo de referência anulável. O compilador não adiciona nenhuma verificação de tempo de execução para tipos de referência não anuláveis. Os benefícios estão na análise de tempo de compilação. O compilador gera avisos que ajudam a localizar e corrigir possíveis erros nulos em seu código. Você declara sua intenção e o compilador avisa quando seu código viola essa intenção.

Em um contexto habilitado para permite valor nulo, o compilador executa uma análise estática em variáveis de qualquer tipo de referência, tanto anulável quanto não anulável. O compilador rastreia o estado nulo de cada variável de referência como *não nulo* ou *talvez seja nulo*. O estado padrão de uma referência não anulável não é *nulo*. O estado padrão de uma referência anulável é *talvez nulo*.

Os tipos de referência não anuláveis devem sempre ser seguros para desreferenciar porque seu estado nulo *não é nulo*. Para impor essa regra, o compilador emite avisos se um tipo de referência não anulável não é inicializado para um valor não nulo. As variáveis locais devem ser atribuídas onde estiverem declaradas. Cada construtor deve atribuir cada campo, em seu corpo, em um construtor chamado ou usando um inicializador de campo. O compilador emite avisos se uma referência não anulável é atribuída a uma referência cujo estado talvez seja *nulo*. No entanto, como uma referência não anulável *não é nula*, nenhum aviso é emitido quando essas variáveis são desreferenciadas.

Tipos de referência anuláveis podem ser inicializados ou atribuídos a `null` . Portanto, a análise estática deve determinar que uma variável *não é nula* antes de ser desreferenciada. Se uma referência anulável for determinada como *talvez nula*, ela não poderá ser atribuída a uma variável de referência não anulável. A classe a seguir mostra exemplos desses avisos:

:::code language="csharp" source="snippets/shared/NullableReferenceTypes.cs" id="SnippetClassWithNullable":::

O trecho a seguir mostra onde o compilador emite avisos ao usar esta classe:

:::code language="csharp" source="snippets/shared/NullableReferenceTypes.cs" id="SnippetLocalWarnings":::

Os exemplos anteriores demonstram a análise estática do compilador para determinar o estado nulo de variáveis de referência. O compilador aplica regras de idioma para verificações e atribuições nulas para informar sua análise.  O compilador não pode fazer suposições sobre a semântica de métodos ou propriedades. Se você chamar métodos que executam verificações nulas, o compilador não poderá saber que esses métodos afetam o estado nulo de uma variável. Há vários atributos que você pode adicionar a suas APIs para informar o compilador sobre a semântica de argumentos e valores de retorno. Esses atributos foram aplicados a muitas APIs comuns nas bibliotecas do .NET Core. Por exemplo, <xref:System.String.IsNullOrEmpty%2A> foi atualizado e o compilador interpreta corretamente esse método como uma verificação nula. Para obter mais informações sobre os atributos que se aplicam à análise estática de estado nulo, consulte o artigo sobre [atributos anuláveis](../attributes/nullable-analysis.md).

## <a name="setting-the-nullable-context"></a>Configurando o contexto anulável

Há duas maneiras de controlar o contexto anulável. No nível do projeto, você pode adicionar a `<Nullable>enable</Nullable>` configuração do projeto. Em um único arquivo de origem C#, você pode adicionar o `#nullable enable` pragma para habilitar o contexto anulável. Consulte o artigo sobre como [definir uma estratégia anulável](../../nullable-migration-strategies.md).

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, consulte as seguintes propostas para a [especificação da linguagem C#](~/_csharplang/spec/introduction.md):

- [Tipos de referência anuláveis](~/_csharplang/proposals/csharp-8.0/nullable-reference-types.md)
- [Especificação de tipos de referência Nullable de rascunho](~/_csharplang/proposals/csharp-9.0/nullable-reference-types-specification.md)

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Tipos de valor anuláveis](nullable-value-types.md)
