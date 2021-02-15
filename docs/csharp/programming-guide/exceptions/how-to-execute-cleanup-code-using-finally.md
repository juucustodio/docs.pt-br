---
title: Como executar o código de limpeza usando o guia de programação finally-C#
description: Saiba como executar o código de limpeza usando uma instrução ' Finally '. As instruções finally garantem que qualquer limpeza necessária de objetos ocorra imediatamente.
ms.date: 12/09/2020
helpviewer_keywords:
- try/finally blocks [C#]
- exceptions [C#], try/finally block
- exception handling [C#], try/finally block
ms.assetid: 1b1e5aef-3f32-4a88-9d39-b5fffb33bdaf
ms.openlocfilehash: e9b5d3086488d3f7e3c0709317d6fafd15c439e8
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110176"
---
# <a name="how-to-execute-cleanup-code-using-finally-c-programming-guide"></a>Como executar o código de limpeza usando finally (guia de programação C#)

O propósito de uma instrução `finally` é garantir que a limpeza necessária de objetos, normalmente objetos que estão mantendo recursos externos, ocorra imediatamente, mesmo que uma exceção seja lançada. Um exemplo dessa limpeza é chamar <xref:System.IO.Stream.Close%2A> em um <xref:System.IO.FileStream> imediatamente após o uso, em vez de esperar que o objeto passe pela coleta de lixo feita pelo Common Language Runtime, da seguinte maneira:

:::code language="csharp" source="snippets/exceptions/Program.cs" ID="NoCleanup":::

## <a name="example"></a>Exemplo

Para transformar o código anterior em uma instrução `try-catch-finally`, o código de limpeza é separado do código funcional, da seguinte maneira.

:::code language="csharp" source="snippets/exceptions/Program.cs" ID="WithCleanup":::

Como uma exceção pode ocorrer a qualquer momento dentro do `try` bloco antes da `OpenWrite()` chamada, ou a `OpenWrite()` chamada em si falhar, não temos certeza de que o arquivo está aberto quando tentamos fechá-lo. O `finally` bloco adiciona uma verificação para certificar-se de que o <xref:System.IO.FileStream> objeto não é `null` antes de chamar o <xref:System.IO.Stream.Close%2A> método. Sem a `null` verificação, o `finally` bloco poderia lançar seu próprio <xref:System.NullReferenceException> , mas gerar exceções em `finally` blocos deve ser evitado se for possível.

Uma conexão de banco de dados é outra boa candidata a ser fechada em um bloco `finally`. Como o número de conexões permitidas para um servidor de banco de dados é, às vezes, limitado, você deve fechar conexões de banco de dados assim que possível. Se uma exceção for lançada antes que você possa fechar a conexão, o uso do `finally` bloco será melhor do que aguardar a coleta de lixo.

## <a name="see-also"></a>Veja também

- [Instrução using](../../language-reference/keywords/using-statement.md)
- [try-catch](../../language-reference/keywords/try-catch.md)
- [try-finally](../../language-reference/keywords/try-finally.md)
- [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)
