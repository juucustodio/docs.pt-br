---
description: 'Saiba mais sobre o tipo de caractere interno em C #'
title: tipo de caractere-referência C#
ms.date: 05/11/2020
f1_keywords:
- char
- char_CSharpKeyword
helpviewer_keywords:
- char data type [C#]
ms.assetid: b51cf4fb-124c-4067-af48-afbac122b228
ms.openlocfilehash: 636e032ac22b48ebc471780ffa85148bf952cdd2
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465085"
---
# <a name="char-c-reference"></a>Char (referência C#)

A `char` palavra-chave Type é um alias para o <xref:System.Char?displayProperty=nameWithType> tipo de estrutura .NET que representa um caractere Unicode UTF-16.

|Tipo|Intervalo|Tamanho|Tipo .NET|
|----------|-----------|----------|-------------------------|
|`char`|U+0000 a U+FFFF|16 bits|<xref:System.Char?displayProperty=nameWithType>|

O valor padrão do `char` tipo é `\0` , ou seja, U + 0000.

O `char` tipo dá suporte a operadores de [comparação](../operators/comparison-operators.md), [igualdade](../operators/equality-operators.md), [incremento](../operators/arithmetic-operators.md#increment-operator-)e [decréscimo](../operators/arithmetic-operators.md#decrement-operator---) . Além disso, para `char` operandos, os operadores [lógicos](../operators/bitwise-and-shift-operators.md) [aritméticos](../operators/arithmetic-operators.md) e de bit-a-vírgula executam uma operação nos códigos de caracteres correspondentes e produzem o resultado do `int` tipo.

O tipo de [cadeia de caracteres](reference-types.md#the-string-type) representa o texto como uma sequência de `char` valores.

## <a name="literals"></a>Literais

Você pode especificar um `char` valor com:

- um literal de caractere.
- uma sequência de escape Unicode, que é `\u` seguida pela representação hexadecimal de quatro símbolos de um código de caractere.
- uma sequência de escape hexadecimal, que é `\x` seguida pela representação hexadecimal de um código de caractere.

[!code-csharp-interactive[char literals](snippets/CharType.cs#Literals)]

Como mostra o exemplo anterior, você também pode converter o valor de um código de caractere no `char` valor correspondente.

> [!NOTE]
> No caso de uma sequência de escape Unicode, você deve especificar todos os quatro dígitos hexadecimais. Ou seja, `\u006A` é uma sequência de escape válida, enquanto `\u06A` e `\u6A` não são válidas.
>
> No caso de uma sequência de escape hexadecimal, você pode omitir os zeros à esquerda. Ou seja, as `\x006A` `\x06A` `\x6A` sequências de escape, e são válidas e correspondem ao mesmo caractere.

## <a name="conversions"></a>Conversões

O `char` tipo é implicitamente conversível nos seguintes tipos [integral](integral-numeric-types.md) : `ushort` ,,, `int` `uint` `long` e `ulong` . Ele também é implicitamente conversível para os tipos numéricos de [ponto flutuante](floating-point-numeric-types.md) internos: `float` , `double` e `decimal` . Ele é explicitamente convertido em `sbyte` , `byte` e `short` tipos integrais.

Não há conversões implícitas de outros tipos para o `char` tipo. No entanto, qualquer tipo [integral](integral-numeric-types.md) ou numérico [de ponto flutuante](floating-point-numeric-types.md) é explicitamente conversível para `char` .

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, consulte a seção [tipos integrais](~/_csharplang/spec/types.md#integral-types) da [especificação da linguagem C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Veja também

- [Referência de C#](../index.md)
- [Tipos de valor](value-types.md)
- [Cadeias de caracteres](../../programming-guide/strings/index.md)
- <xref:System.Text.Rune?displayProperty=nameWithType>
- [Codificação de caracteres no .NET](../../../standard/base-types/character-encoding-introduction.md)
