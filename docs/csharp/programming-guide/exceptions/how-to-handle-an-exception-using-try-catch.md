---
title: Como tratar uma exceção usando o guia de programação do try-catch-C#
description: Saiba como tratar uma exceção usando um bloco try-catch. Consulte um exemplo de código e exiba recursos adicionais disponíveis.
ms.date: 12/09/2020
helpviewer_keywords:
- exception handling [C#], try/catch blocks
- exceptions [C#], try/catch blocks
- try/catch blocks [C#]
ms.assetid: ca8e3773-980e-4767-8633-7408540e9818
ms.openlocfilehash: b6368660dbe037123f5bb6ce52502d4a94fcfc3a
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110514"
---
# <a name="how-to-handle-an-exception-using-trycatch-c-programming-guide"></a>Como tratar uma exceção usando try/catch (guia de programação C#)

A finalidade de um bloco [try-catch](../../language-reference/keywords/try-catch.md) é capturar e manipular uma exceção gerada pelo código de trabalho. Algumas exceções podem ser tratadas em um `catch` bloco e o problema é resolvido sem que a exceção seja relançada; no entanto, com mais frequência a única coisa que você pode fazer é verificar se a exceção apropriada foi lançada.

## <a name="example"></a>Exemplo

Neste exemplo, <xref:System.IndexOutOfRangeException> não é a exceção mais apropriada: <xref:System.ArgumentOutOfRangeException> faz mais sentido para o método porque o erro é causado pelo `index` argumento passado pelo chamador.

:::code language="csharp" source="snippets/exceptions/ExampleTryCatch.cs" id="ExampleTryCatch":::

## <a name="comments"></a>Comentários

O código que causa uma exceção fica dentro do bloco `try`. A instrução `catch` é adicionada logo após para manipular `IndexOutOfRangeException`, se ocorrer. O bloco `catch` manipula o `IndexOutOfRangeException` e gera a exceção `ArgumentOutOfRangeException`, que é mais adequada. Para fornecer ao chamador tantas informações quanto possível, considere especificar a exceção original como o <xref:System.Exception.InnerException%2A> da nova exceção. Como a <xref:System.Exception.InnerException%2A> propriedade é [somente leitura](../../properties.md#read-only), você deve atribuí-la no construtor da nova exceção.
