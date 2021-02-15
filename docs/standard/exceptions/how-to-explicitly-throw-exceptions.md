---
title: Como lançar exceções explicitamente
description: Saiba como lançar uma exceção explicitamente no .NET usando a instrução C# throw ou a instrução Visual Basic throw.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- exceptions, try/catch blocks
- FileNotFoundException class
- try/catch blocks
- exceptions, throwing
- implicitly throwing exceptions
ms.assetid: 72bdd157-caa9-4478-9ee3-cb4500b84528
ms.openlocfilehash: 37ba5f952d621ff2e209a3bac375b62894c944a7
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828043"
---
# <a name="how-to-explicitly-throw-exceptions"></a>Como gerar exceções explicitamente

Você pode lançar uma exceção explicitamente usando o C# [`throw`](../../csharp/language-reference/keywords/throw.md) ou a [`Throw`](../../visual-basic/language-reference/statements/throw-statement.md) instrução Visual Basic. Você também pode lançar novamente uma exceção capturada usando a instrução `throw`. É uma boa prática adicionar informações a uma exceção que é lançada novamente para fornecer mais informações durante a depuração.

O exemplo de código a seguir usa um bloco `try`/`catch` para capturar uma possível <xref:System.IO.FileNotFoundException>. Após o bloco `try`, há um bloco `catch` que captura a <xref:System.IO.FileNotFoundException> e grava uma mensagem no console se o arquivo de dados não é encontrado. A próxima instrução é a instrução `throw`, que gera uma nova <xref:System.IO.FileNotFoundException> e adiciona informações de texto à exceção.

[!code-csharp[Exception.Throwing#1](~/samples/snippets/csharp/VS_Snippets_CLR/Exception.Throwing/CS/throw.cs#1)]
[!code-vb[Exception.Throwing#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/Exception.Throwing/VB/throw.vb#1)]  

## <a name="see-also"></a>Confira também

- [Exceções](index.md)
