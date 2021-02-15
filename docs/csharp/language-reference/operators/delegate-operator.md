---
description: operador delegate – referência do C#
title: operador delegate – referência do C#
ms.date: 09/25/2020
helpviewer_keywords:
- delegate [C#]
- anonymous method [C#]
ms.openlocfilehash: db2bf673db12e4a10741a26112820726a4b8aaee
ms.sourcegitcommit: c04535ad05e374fb269fcfc6509217755fbc0d54
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91247651"
---
# <a name="delegate-operator-c-reference"></a>operador delegate (referência do C#)

O operador `delegate` cria um método anônimo que pode ser convertido em um tipo delegado:

[!code-csharp-interactive[anonymous method](snippets/shared/DelegateOperator.cs#AnonymousMethod)]

> [!NOTE]
> Começando com o C# 3, as expressões lambda fornecem uma maneira mais concisa e expressiva de criar uma função anônima. Use o [operador =>](lambda-operator.md) para construir uma expressão lambda:
>
> [!code-csharp-interactive[lambda expression](snippets/shared/DelegateOperator.cs#Lambda)]
>
> Para saber mais sobre recursos de expressões lambda, por exemplo, que capturam variáveis externas, confira [Expressões lambda](lambda-expressions.md).

Você pode omitir a lista de parâmetros quando usa o operador `delegate`. Se você fizer isso, o método anônimo criado poderá ser convertido em um tipo delegado com qualquer lista de parâmetros, como mostra o exemplo a seguir:

[!code-csharp-interactive[no parameter list](snippets/shared/DelegateOperator.cs#WithoutParameterList)]

Essa é a única funcionalidade de métodos anônimos que não tem suporte por expressões lambda. Em todos os outros casos, uma expressão lambda é a forma preferida de gravar código embutido.

A partir do C# 9,0, você pode usar os [Descartes](../../discards.md) para especificar dois ou mais parâmetros de entrada de um método anônimo que não são usados pelo método:

:::code language="csharp" source="snippets/shared/DelegateOperator.cs" id="SnippetDiscards" :::

Para compatibilidade com versões anteriores, se apenas um único parâmetro for nomeado `_` , `_` será tratado como o nome desse parâmetro dentro de um método anônimo.

Além de começar com o C# 9,0, você pode usar o `static` modificador na declaração de um método anônimo:

:::code language="csharp" source="snippets/shared/DelegateOperator.cs" id="SnippetStatic" :::

Um método anônimo estático não pode capturar variáveis locais ou estado de instância de escopos delimitadores.

Você também usa a palavra-chave `delegate` para declarar um [tipo delegado](../builtin-types/reference-types.md#the-delegate-type).

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, confira a seção [Expressões de função anônima](~/_csharplang/spec/expressions.md#anonymous-function-expressions) da [Especificação da linguagem C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Operadores e expressões C#](index.md)
- [= Operador de>](lambda-operator.md)
