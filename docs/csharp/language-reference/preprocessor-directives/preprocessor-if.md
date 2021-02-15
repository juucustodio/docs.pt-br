---
description: '#Diretiva de pré-processamento "if" – Referência de C#'
title: '#Diretiva de pré-processamento "if" – Referência de C#'
ms.date: 10/27/2019
f1_keywords:
- '#if'
helpviewer_keywords:
- '#if directive [C#]'
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
ms.openlocfilehash: dc3e235db49279691203a0db4d124239fb972c69
ms.sourcegitcommit: a69d548f90a03e105ee6701236c38390ecd9ccd1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90065222"
---
# <a name="if-c-reference"></a>#if (referência C#)

Quando o Compilador do Visual C# encontra uma diretiva `#if`, seguida eventualmente por uma diretiva [#endif](preprocessor-endif.md), ele compila o código entre as diretivas somente quando o símbolo especificado é definido. Ao contrário do C e do C++, não é possível atribuir um valor numérico a um símbolo. A `#if` instrução em C# é booliana e só testa se o símbolo foi definido ou não. Por exemplo:

```csharp
#if DEBUG
    Console.WriteLine("Debug version");
#endif
```

Você pode usar os operadores [==](../operators/equality-operators.md#equality-operator-) (igualdade) e [! =](../operators/equality-operators.md#inequality-operator-) (desigualdade) somente para testar os valores [bool](../builtin-types/bool.md) `true` ou `false` . `true` significa que o símbolo está definido. A instrução `#if DEBUG` tem o mesmo significado que `#if (DEBUG == true)`. Você pode usar a [&&  (and)](../operators/boolean-logical-operators.md#conditional-logical-and-operator-), [&#124;&#124;  (ou)](../operators/boolean-logical-operators.md#conditional-logical-or-operator-)e [! (não)](../operators/boolean-logical-operators.md#logical-negation-operator-) operadores para avaliar se vários símbolos foram definidos. Também é possível agrupar os símbolos e operadores com parênteses.

## <a name="remarks"></a>Comentários

`#if`junto com as diretivas [#else](preprocessor-else.md), [#elif](preprocessor-elif.md), [#endif](preprocessor-endif.md), [#define](preprocessor-define.md)e [#undef](preprocessor-undef.md) , permite que você inclua ou exclua o código com base na existência de um ou mais símbolos. Isso pode ser útil ao compilar o código para um build de depuração ou ao compilar para uma configuração específica.

Uma diretiva condicional que começa com uma diretiva `#if` deverá ser explicitamente encerrada com uma diretiva `#endif`.

A diretiva `#define` permite definir um símbolo. Ao usar o símbolo como a expressão passada para a diretiva `#if`, a expressão será avaliada como `true`.

Você também pode definir um símbolo com a opção [-definir](../compiler-options/define-compiler-option.md) compilador. É possível excluir um símbolo com [#undef](preprocessor-undef.md).

Um símbolo definido com `-define` ou com `#define` não entra em conflito com uma variável do mesmo nome. Ou seja, um nome de variável não deve ser passado para uma diretiva de pré-processamento e um símbolo pode ser avaliado apenas por uma diretiva de pré-processamento.

O escopo de um símbolo criado com `#define` é o arquivo no qual ele foi definido.

O sistema de compilação também reconhece os símbolos de pré-processador predefinidos que representam [estruturas de destino](../../../standard/frameworks.md) diferentes em projetos em estilo SDK. Eles são úteis ao criar aplicativos que podem ter como destino mais de uma versão do .NET.

[!INCLUDE [Preprocessor symbols](~/includes/preprocessor-symbols.md)]

> [!NOTE]
> Para projetos tradicionais de estilo não-SDK, você precisa configurar manualmente os símbolos de compilação condicional para as diferentes estruturas de destino no Visual Studio por meio das páginas de propriedades do projeto.

As constantes TRACE e DEBUG são exemplos de outros símbolos predefinidos. Para substituir os valores definidos no projeto, use a diretiva `#define`. Por exemplo, o símbolo DEBUG é definido automaticamente, de acordo com as propriedades de configuração do build (Modo de Depuração ou Modo de Versão).

## <a name="examples"></a>Exemplos

O exemplo a seguir mostra como definir um símbolo MYTEST em um arquivo e testar os valores dos símbolos MYTEST e DEBUG. A saída deste exemplo depende do fato de você criar o projeto no modo de configuração de versão ou no modo de configuração de depuração.

```csharp
#define MYTEST
using System;
public class MyClass
{
    static void Main()
    {
#if (DEBUG && !MYTEST)
        Console.WriteLine("DEBUG is defined");
#elif (!DEBUG && MYTEST)
        Console.WriteLine("MYTEST is defined");
#elif (DEBUG && MYTEST)
        Console.WriteLine("DEBUG and MYTEST are defined");  
#else
        Console.WriteLine("DEBUG and MYTEST are not defined");
#endif
    }
}
```

O exemplo a seguir mostra como testar várias estruturas de destino para que você possa usar APIs mais recentes, quando possível:

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        WebClient _client = new WebClient();
#else
        HttpClient _client = new HttpClient();
#endif
    }
    //...
}
```

## <a name="see-also"></a>Veja também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](index.md)
- [Como: compilar condicionalmente com Trace e Debug](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)
