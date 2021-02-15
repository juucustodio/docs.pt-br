---
title: Manipulação de exceções – Guia de Programação em C#
description: Saiba mais sobre manipulação de exceção. Veja exemplos de instruções Try-Catch, try-finally e try-catch-finally.
ms.date: 12/09/2020
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], handling
ms.assetid: b4e4ecf2-b907-4e58-891f-2563762258e9
ms.openlocfilehash: fabf1413ba498232e67f45460195fe96e25fab0a
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110189"
---
# <a name="exception-handling-c-programming-guide"></a>Manipulação de exceções (Guia de Programação em C#)

Um bloco [try](../../language-reference/keywords/try-catch.md) é usado por programadores de C# para particionar o código que pode ser afetado por uma exceção. Os blocos [catch](../../language-reference/keywords/try-catch.md) associados são usados para tratar qualquer exceção resultante. Um bloco [finally](../../language-reference/keywords/try-finally.md) contém código que é executado independentemente de uma exceção ser gerada ou não no `try` bloco, como liberar recursos que são alocados no `try` bloco. Um bloco `try` exige um ou mais blocos `catch` associados ou um bloco `finally` ou ambos.

Os exemplos a seguir mostram uma instrução `try-catch`, uma instrução `try-finally` e um instrução `try-catch-finally`.

:::code language="csharp" source="snippets/exceptions/Program.cs" id="TryCatchStructure":::

:::code language="csharp" source="snippets/exceptions/Program.cs" id="TryFinallyStructure":::

:::code language="csharp" source="snippets/exceptions/Program.cs" id="TryCatchFinallyStructure":::

Um bloco `try` sem um bloco `catch` ou `finally` causa um erro do compilador.

## <a name="catch-blocks"></a>Blocos catch

Um bloco `catch` pode especificar o tipo de exceção a ser capturado. A especificação de tipo é chamada de *filtro de exceção*. O tipo de exceção deve ser derivado de <xref:System.Exception>. Em geral, não especifique <xref:System.Exception> como o filtro de exceção, a menos que você saiba como lidar com todas as exceções que podem ser geradas no `try` bloco ou tenha incluído uma instrução [throw](../../language-reference/keywords/throw.md) no final do `catch` bloco.

Vários `catch` blocos com classes de exceção diferentes podem ser encadeados juntos. Os blocos `catch` são avaliados de cima para baixo no seu código, mas somente um bloco `catch` será executado para cada exceção que é lançada. O primeiro bloco `catch` que especifica o tipo exato ou uma classe base da exceção lançada será executado. Se nenhum `catch` bloco especificar uma classe de exceção correspondente, um `catch` bloco que não tem nenhum tipo será selecionado, se um estiver presente na instrução. É importante posicionar `catch` blocos com as classes de exceção mais específicas (ou seja, as mais derivadas) primeiro.

Capturar exceções quando as seguintes condições forem verdadeiras:

- Você tem uma boa compreensão de porque a exceção seria lançada e pode implementar uma recuperação específica, como solicitar que o usuário insira um novo nome de arquivo, quando você capturar um objeto <xref:System.IO.FileNotFoundException>.
- Você pode criar e lançar uma exceção nova e mais específica.
  :::code language="csharp" source="snippets/exceptions/Program.cs" id="ThrowMoreSpecificException":::
- Você deseja tratar parcialmente uma exceção antes de passá-la para tratamento adicional. No exemplo a seguir, um `catch` bloco é usado para adicionar uma entrada a um log de erros antes de relançar a exceção.
  :::code language="csharp" source="snippets/exceptions/Program.cs" id="RethrowError":::

Você também pode especificar *filtros de exceção* para adicionar uma expressão booliana a uma cláusula catch. Eles indicam que uma cláusula catch específica corresponde somente quando essa condição é verdadeira. No exemplo a seguir, ambas as cláusulas catch usam a mesma classe de exceção, mas uma condição adicional é verificada para criar uma mensagem de erro diferente:

:::code language="csharp" source="snippets/exceptions/ExceptionFilter.cs" ID="DemonstrateExceptionFilter":::

Um filtro de exceção que sempre retorna `false` pode ser usado para examinar todas as exceções, mas não processá-las. Um uso típico é registrar exceções:

:::code language="csharp" source="snippets/exceptions/ExceptionFilter.cs" ID="ShowExceptionFilter":::

O `LogException` método sempre retorna `false` , nenhuma `catch` cláusula usando este filtro de exceção corresponde. A cláusula catch pode ser geral, usando <xref:System.Exception?displayProperty=nameWithType> , e as cláusulas posteriores podem processar classes de exceção mais específicas.

## <a name="finally-blocks"></a>Blocos Finally

Um bloco `finally` permite que você limpe as ações que são realizadas em um bloco `try`. Se estiver presente, o bloco `finally` será executado por último, depois do bloco `try` e de qualquer bloco `catch` de correspondência. Um `finally` bloco sempre é executado, se uma exceção é lançada ou se um `catch` bloco correspondente ao tipo de exceção é encontrado.

O bloco `finally` pode ser usado para liberar recursos, como fluxos de arquivos, conexões de banco de dados e identificadores de gráficos, sem esperar que o coletor de lixo no runtime finalize os objetos. Para obter mais informações, consulte a [instrução using](../../language-reference/keywords/using-statement.md).

No exemplo a seguir, o bloco `finally` é usado para fechar um arquivo está aberto no bloco `try`. Observe que o estado do identificador de arquivo é selecionado antes do arquivo ser fechado. Se o `try` bloco não puder abrir o arquivo, o identificador de arquivo ainda terá o valor `null` e o `finally` bloco não tentará fechá-lo. Em vez disso, se o arquivo for aberto com êxito no `try` bloco, o `finally` bloco fechará o arquivo aberto.

:::code language="csharp" source="snippets/exceptions/Program.cs" id="CleanupIfNotNull":::

## <a name="c-language-specification"></a>Especificação da Linguagem C#

Para obter mais informações, veja [Exceções](~/_csharplang/spec/exceptions.md) e [A declaração try](~/_csharplang/spec/statements.md#the-try-statement) na [Especificação da Linguagem C#](/dotnet/csharp/language-reference/language-specification/introduction). A especificação da linguagem é a fonte definitiva para a sintaxe e o uso de C#.
  
## <a name="see-also"></a>Veja também

- [Referência do C#](../../language-reference/index.md)
- [try-catch](../../language-reference/keywords/try-catch.md)
- [try-finally](../../language-reference/keywords/try-finally.md)
- [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)
- [Instrução using](../../language-reference/keywords/using-statement.md)
