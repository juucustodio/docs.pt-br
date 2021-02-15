---
title: Exceções e manipulação de exceções – Guia de Programação em C#
description: Saiba mais sobre exceções e tratamento de exceções. Esses recursos do C# ajudam a lidar com situações inesperadas ou excepcionais que ocorrem quando um programa está em execução.
ms.date: 12/09/2020
helpviewer_keywords:
- exception handling [C#]
- exceptions [C#]
- C# language, exceptions
ms.assetid: 0001887f-4fa2-47e2-8034-2819477e2344
ms.openlocfilehash: 679171e6d397741ef44cb37fb770f6feba039fd9
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110618"
---
# <a name="exceptions-and-exception-handling-c-programming-guide"></a>Exceções e manipulação de exceções (Guia de Programação em C#)

Os recursos de manipulação de exceção da linguagem C# ajudam você a lidar com quaisquer situações excepcionais ou inesperadas que ocorram quando um programa for executado. A manipulação de exceções usa as `try` `catch` `finally` palavras-chave, e para testar as ações que podem não ter sucesso, para lidar com falhas quando você decide que é razoável fazê-lo e para limpar os recursos posteriormente. As exceções podem ser geradas pelo Common Language Runtime (CLR), por bibliotecas .NET ou de terceiros, ou por código de aplicativo. As exceções são criadas usando a palavra-chave `throw`.

Em muitos casos, uma exceção pode ser lançada não por um método que seu código chamou diretamente, mas por outro método mais abaixo na pilha de chamadas. Quando uma exceção é gerada, o CLR desenrolará a pilha, procurando um método com um `catch` bloco para o tipo de exceção específico e executará o primeiro `catch` bloco desse bloqueio que, se encontrar. Se ele não encontrar um bloco `catch` apropriado na pilha de chamadas, ele encerrará o processo e exibirá uma mensagem para o usuário.

Neste exemplo, um método testa a divisão por zero e captura o erro. Sem a manipulação de exceção, esse programa encerraria com um **DivideByZeroException não resolvido**.

:::code language="csharp" source="snippets/exceptions/ExceptionTest.cs" ID="ExceptionTest":::

## <a name="exceptions-overview"></a>Visão geral sobre exceções

As exceções têm as seguintes propriedades:

- As exceções são tipos que derivam, por fim, de `System.Exception`.
- Use um bloco `try` nas instruções que podem lançar exceções.
- Quando ocorre uma exceção no bloco `try`, o fluxo de controle vai para o primeiro manipulador de exceção associada que está presente em qualquer lugar na pilha de chamadas. No C#, a palavra-chave `catch` é usada para definir um manipulador de exceção.
- Se nenhum manipulador de exceção para uma determinada exceção estiver presente, o programa interromperá a execução com uma mensagem de erro.
- Não Capture uma exceção, a menos que você possa tratá-la e deixar o aplicativo em um estado conhecido. Se você capturar `System.Exception`, relance-o usando a palavra-chave `throw` no final do bloco `catch`.
- Se um bloco `catch` define uma variável de exceção, você pode usá-lo para obter mais informações sobre o tipo de exceção que ocorreu.
- As exceções podem ser geradas explicitamente por um programa usando a palavra-chave `throw`.
- Os objetos de exceção contêm informações detalhadas sobre o erro, como o estado da pilha de chamadas e uma descrição de texto do erro.
- O código em um bloco `finally` será executado mesmo se uma exceção for lançada. Use um bloco `finally` para liberar recursos, por exemplo, para fechar todos os fluxos ou arquivos que foram abertos no bloco `try`.
- As exceções gerenciadas no .NET são implementadas sobre o mecanismo de manipulação de exceção estruturada do Win32. Para obter mais informações, consulte [Manipulação de exceções estruturadas (C/C++)](/cpp/cpp/structured-exception-handling-c-cpp) e [Curso rápido sobre a manipulação de exceções estruturadas do Win32](http://bytepointer.com/resources/pietrek_crash_course_depths_of_win32_seh.htm).

## <a name="c-language-specification"></a>Especificação da Linguagem C#

Para obter mais informações, veja [Exceções](~/_csharplang/spec/exceptions.md) na [Especificação da linguagem C#](/dotnet/csharp/language-reference/language-specification/introduction). A especificação da linguagem é a fonte definitiva para a sintaxe e o uso de C#.

## <a name="see-also"></a>Veja também

- <xref:System.SystemException>
- [Palavras-chave do C#](../../language-reference/keywords/index.md)
- [throw](../../language-reference/keywords/throw.md)
- [try-catch](../../language-reference/keywords/try-catch.md)
- [try-finally](../../language-reference/keywords/try-finally.md)
- [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)
- [Exceções](../../../standard/exceptions/index.md)
