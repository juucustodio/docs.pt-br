---
title: Usando exceções – Guia de Programação em C#
description: Saiba como usar exceções. As exceções são geradas pelo código que encontra um erro e detectadas pelo código que corrige o erro.
ms.date: 12/09/2020
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], about exceptions
ms.assetid: 71472c62-320a-470a-97d2-67995180389d
ms.openlocfilehash: 30a7c3eecb599493dfa74d664c4899836c1b9276
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110215"
---
# <a name="use-exceptions-c-programming-guide"></a>Usar exceções (guia de programação C#)

No C#, os erros no programa em tempo de execução são propagados pelo programa usando um mecanismo chamado exceções. As exceções são geradas pelo código que encontra um erro e capturadas pelo código que pode corrigir o erro. As exceções podem ser geradas pelo tempo de execução do .NET ou pelo código em um programa. Uma vez que uma exceção é gerada, ela é propagada acima na pilha de chamadas até uma instrução `catch` para a exceção ser encontrada. As exceções não capturadas são tratadas por um manipulador de exceção genérico fornecido pelo sistema que exibe uma caixa de diálogo.

As exceções são representadas por classes derivadas de <xref:System.Exception>. Essa classe identifica o tipo de exceção e contém propriedades que têm detalhes sobre a exceção. Gerar uma exceção envolve criar uma instância de uma classe derivada de exceção, opcionalmente configurar propriedades da exceção e, em seguida, gerar o objeto usando a palavra-chave `throw`. Por exemplo:

:::code language="csharp" source="snippets/exceptions/Program.cs" id="ThrowException":::

Depois que uma exceção é gerada, o runtime verifica a instrução atual para ver se ela está dentro de um bloco `try`. Se estiver, todos os blocos `catch` associados ao bloco `try` serão verificados para ver se eles podem capturar a exceção. Os blocos `Catch` normalmente especificam os tipos de exceção. Se o tipo do bloco `catch` for do mesmo tipo que a exceção ou uma classe base da exceção, o bloco `catch` poderá manipular o método. Por exemplo:

:::code language="csharp" source="snippets/exceptions/Program.cs" id="CatchException":::

Se a instrução que gera uma exceção não está dentro de um `try` bloco ou se o `try` bloco que o inclui não tem nenhum `catch` bloco correspondente, o tempo de execução verifica o método de chamada para uma `try` instrução e `catch` blocos. O runtime continuará acima na pilha de chamada, pesquisando um bloco `catch` compatível. Depois que o bloco `catch` for localizado e executado, o controle será passado para a próxima instrução após aquele bloco `catch`.

Uma instrução `try` pode conter mais de um bloco `catch`. A primeira `catch` instrução que pode manipular a exceção é executada; qualquer instrução a seguir `catch` , mesmo se for compatível, será ignorada. Os blocos catch devem ser sempre ordenados do mais específico (ou mais derivado) para o menos específico. Por exemplo:

:::code language="csharp" source="snippets/exceptions/CatchOrder.cs":::

Antes de o bloco `catch` ser executado, o runtime verifica se há blocos `finally`. `Finally` os blocos permitem que o programador limpe qualquer estado ambíguo que pudesse ser deixado de um bloco anulado `try` ou libere recursos externos (como identificadores gráficos, conexões de banco de dados ou fluxos de arquivos) sem esperar que o coletor de lixo no tempo de execução Finalize os objetos. Por exemplo:

:::code language="csharp" source="snippets/exceptions/Program.cs" id="TestFinally":::

Se `WriteByte()` o lançou uma exceção, o código no segundo `try` bloco que tentar reabrir o arquivo falhará se `file.Close()` não for chamado, e o arquivo permanecerá bloqueado. Como os blocos `finally` são executados mesmo se uma exceção for gerada, o bloco `finally` no exemplo anterior permite que o arquivo seja fechado corretamente e ajuda a evitar um erro.

Se não for encontrado nenhum bloco `catch` compatível na pilha de chamadas após uma exceção ser gerada, ocorrerá uma das três coisas:

- Se a exceção estiver em um finalizador, o finalizador será anulado e o finalizador base, se houver, será chamado.
- Se a pilha de chamadas contiver um construtor estático ou um inicializador de campo estático, uma <xref:System.TypeInitializationException> será gerada, com a exceção original atribuída à propriedade <xref:System.Exception.InnerException%2A> da nova exceção.
- Se o início do thread for atingido, o thread será encerrado.
