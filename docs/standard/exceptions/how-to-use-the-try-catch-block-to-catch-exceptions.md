---
title: Como usar o bloco try-catch para capturar exceções
description: Use o bloco try para conter instruções que podem gerar ou gerar uma exceção. Coloque instruções para manipular exceções em um ou mais blocos catch.
ms.date: 02/06/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- exceptions, try/catch blocks
- try blocks
- try/catch blocks
- catch blocks
ms.assetid: a3ce6dfd-1f64-471b-8ad8-8cfaf406275d
ms.openlocfilehash: cfe5b2b304cdb9efe7f0d91059fe1c279b4fa2dd
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828004"
---
# <a name="how-to-use-the-trycatch-block-to-catch-exceptions"></a>Como usar o bloco try/catch para capturar exceções

Colocar todas as instruções de código que podem elevar ou gerar uma exceção em um bloco `try` e posicionar instruções usadas para tratar a exceção ou exceções em um ou mais blocos `catch` abaixo do bloco `try`. Cada bloco `catch` inclui o tipo de exceção e pode conter instruções adicionais necessárias para lidar com esse tipo de exceção.

No exemplo a seguir, um <xref:System.IO.StreamReader> abre um arquivo chamado *data.txt* e recupera uma linha desse arquivo. Uma vez que o código pode gerar qualquer uma de três exceções, ele é colocado em um bloco `try`. Três blocos `catch` capturam as exceções e lidam com elas, exibindo os resultados no console.

[!code-csharp[CatchException#3](~/samples/snippets/csharp/VS_Snippets_CLR/CatchException/CS/catchexception2.cs#3)]
[!code-vb[CatchException#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/CatchException/VB/catchexception2.vb#3)]

O CLR (Common Language Runtime) captura exceções não manipuladas pelos blocos `catch`. Se uma exceção é capturada pelo CLR, um dos seguintes resultados pode ocorrer dependendo da configuração do CLR:

- Uma caixa de diálogo **Depurar** é exibida.
- O programa interromperá a execução e uma caixa de diálogo será exibida com informações de exceção.
- Um erro é impresso no [fluxo de saída de erro padrão](xref:System.Console.Error).

> [!NOTE]
> A maioria dos códigos pode lançar uma exceção, sendo que algumas exceções, tais como <xref:System.OutOfMemoryException>, podem ser geradas pelo próprio CLR, a qualquer momento. Embora os aplicativos não precisem lidar com essas exceções, esteja ciente dessa possibilidade ao gravar bibliotecas para serem usadas por outros. Para obter sugestões sobre quando definir código em um bloco `try`, confira [Práticas recomendadas para exceções](best-practices-for-exceptions.md).

## <a name="see-also"></a>Confira também

- [Exceções](index.md)
- [Tratamento de erros de E/S no .NET](../io/handling-io-errors.md)
