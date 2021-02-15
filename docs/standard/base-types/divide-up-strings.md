---
title: Separar cadeias de caracteres em subcadeias
description: Saiba mais sobre técnicas diferentes para extrair partes de uma cadeia de caracteres, incluindo String. Split, expressões regulares e String. substring.
ms.date: 10/30/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET], breaking up
ms.openlocfilehash: b753476b7d8e5808fdcacc6f28bd1de5f8b232bb
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829643"
---
# <a name="extract-substrings-from-a-string"></a>Extrair subcadeias de uma cadeia de caracteres

Este artigo aborda algumas técnicas diferentes para extrair partes de uma cadeia de caracteres.

- Use o [método Split](#stringsplit-method) quando as subcadeias de caracteres desejadas estiverem separadas por um caractere delimitador conhecido (ou caracteres).
- As [expressões regulares](#regular-expressions) são úteis quando a cadeia de caracteres está de acordo com um padrão fixo.
- Use os [métodos IndexOf e substring](#stringindexof-and-stringsubstring-methods) em conjunto quando você não quiser extrair *todas* as subcadeias de caracteres em uma cadeia de caracteres.

## <a name="stringsplit-method"></a>Método String. Split

<xref:System.String.Split%2A?displayProperty=nameWithType> fornece uma série de sobrecargas para ajudá-lo a dividir uma cadeia de caracteres em um grupo de subcadeias de caracteres com base em um ou mais caractere delimitador que você especificar. Você pode optar por limitar o número total de subcadeias de caracteres no resultado final, aparar caracteres de espaço em branco de subcadeias ou excluir subcadeias de caracteres vazias.

Os exemplos a seguir mostram três sobrecargas diferentes de `String.Split()` . O primeiro exemplo chama a <xref:System.String.Split(System.Char[])> sobrecarga sem passar nenhum caractere separador. Quando você não especifica nenhum caractere delimitador, `String.Split()` o usa delimitadores padrão, que são caracteres de espaço em branco, para dividir a cadeia de caracteres.

[!code-csharp-interactive[Intro#1](snippets/parse-strings/csharp/intro.cs#1)]
:::code language="vb" source="snippets/parse-strings/vb/intro.vb" id="1":::

Como você pode ver, os caracteres de ponto ( `.` ) são incluídos em duas das subcadeias de caracteres. Se você quiser excluir os caracteres de período, poderá adicionar o caractere de ponto como um caractere de delimitação adicional. O exemplo a seguir mostra como fazer isso.

[!code-csharp-interactive[Intro#1](snippets/parse-strings/csharp/intro.cs#2)]
:::code language="vb" source="snippets/parse-strings/vb/intro.vb" id="2":::

Os períodos foram removidas das subcadeias de caracteres, mas agora duas subcadeias vazias extras foram incluídas. Essas subcadeias de caracteres vazias representam a subcadeia de caracteres entre a palavra e o período que a segue. Para omitir subcadeias de caracteres vazias da matriz resultante, você pode chamar a <xref:System.String.Split(System.Char[],System.StringSplitOptions)> sobrecarga e especificar <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> para o `options` parâmetro.

[!code-csharp-interactive[Intro#1](snippets/parse-strings/csharp/intro.cs#3)]
:::code language="vb" source="snippets/parse-strings/vb/intro.vb" id="3":::

## <a name="regular-expressions"></a>Expressões regulares

Se a cadeia de caracteres estiver em conformidade com um padrão fixo, você poderá usar uma expressão regular para extrair e manipular seus elementos. Por exemplo, se cadeias de caracteres assumirem o formato " *número* do *operando* de *número* ", você poderá usar uma [expressão regular](regular-expressions.md) para extrair e manipular os elementos da cadeia de caracteres. Aqui está um exemplo:

:::code language="csharp" source="snippets/parse-strings/csharp/regex.cs" id="1" interactive="try-dotnet":::
:::code language="vb" source="snippets/parse-strings/vb/regex.vb" id="1":::

O padrão de expressão regular `(\d+)\s+([-+*/])\s+(\d+)` é definido da seguinte maneira:

|Padrão|Descrição|
|-------------|-----------------|
|`(\d+)`|Corresponde a um ou mais dígitos decimais. Este é o primeiro grupo de captura.|
|`\s+`|Corresponder um ou mais caracteres de espaço em branco.|
|`([-+*/])`|Corresponder um sinal de operador aritmético (+,-, * ou/). Este é o segundo grupo de captura.|
|`\s+`|Corresponder um ou mais caracteres de espaço em branco.|
|`(\d+)`|Corresponde a um ou mais dígitos decimais. Este é o terceiro grupo de captura.|

Você também pode usar uma expressão regular para extrair subseqüências de uma cadeia de caracteres com base em um padrão, em vez de um conjunto fixo de caracteres. Esse é um cenário comum quando uma dessas condições ocorre:

- Um ou mais dos caracteres delimitadores nem *sempre* servem como um delimitador na <xref:System.String> instância.

- A sequência e o número de caracteres do delimitador são variáveis ou são desconhecidos.

Por exemplo, o <xref:System.String.Split%2A> método não pode ser usado para dividir a cadeia de caracteres a seguir, porque o número de `\n` caracteres (nova linha) é variável e nem sempre funciona como delimitadores.

```text
[This is captured\ntext.]\n\n[\n[This is more captured text.]\n]
\n[Some more captured text:\n   Option1\n   Option2][Terse text.]
```

Uma expressão regular pode dividir essa cadeia de caracteres facilmente, como mostra o exemplo a seguir.

:::code language="csharp" source="snippets/parse-strings/csharp/regex.cs" id="2" interactive="try-dotnet":::
:::code language="vb" source="snippets/parse-strings/vb/regex.vb" id="2":::

O padrão de expressão regular `\[([^\[\]]+)\]` é definido da seguinte maneira:

|Padrão|Descrição|
|-------------|-----------------|
|`\[`|Corresponde a um colchete de abertura.|
|`([^\[\]]+)`|Corresponder qualquer caractere que não seja um colchete de abertura ou de fechamento uma ou mais vezes. Este é o primeiro grupo de captura.|
|`\]`|Corresponde a um colchete de fechamento.|

O <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> método é quase idêntico ao <xref:System.String.Split%2A?displayProperty=nameWithType> , exceto pelo fato de que ele divide uma cadeia de caracteres com base em um padrão de expressão regular em vez de um conjunto de caracteres fixo. Por exemplo, o exemplo a seguir usa o <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> método para dividir uma cadeia de caracteres que contém subcadeias de caracteres delimitadas por várias combinações de hifens e outros caracteres.

:::code language="csharp" source="snippets/parse-strings/csharp/regex.cs" id="3" interactive="try-dotnet":::
:::code language="vb" source="snippets/parse-strings/vb/regex.vb" id="3":::

O padrão de expressão regular `\s-\s?[+*]?\s?-\s` é definido da seguinte maneira:

|Padrão|Descrição|
|-------------|-----------------|
|`\s-`|Corresponder a um caractere de espaço em branco seguido por um hífen.|
|`\s?`|Corresponder a zero ou a um caractere de espaço em branco.|
|`[+*]?`|Corresponder a zero ou uma ocorrência do caractere + ou *.|
|`\s?`|Corresponder a zero ou a um caractere de espaço em branco.|
|`-\s`|Corresponder um hífen seguido por um caractere de espaço em branco.|

## <a name="stringindexof-and-stringsubstring-methods"></a>Métodos String. IndexOf e String. substring

Se você não estiver interessado em todas as subcadeias em uma cadeia de caracteres, talvez prefira trabalhar com um dos métodos de comparação de cadeia de caracteres que retorna o índice no qual a correspondência começa. Em seguida, você pode chamar o <xref:System.String.Substring%2A> método para extrair a subcadeia de caracteres desejada. Os métodos de comparação de cadeia de caracteres incluem:

- <xref:System.String.IndexOf%2A>, que retorna o índice de base zero da primeira ocorrência de um caractere ou uma cadeia de caracteres em uma instância de cadeia de caracteres.

- <xref:System.String.IndexOfAny%2A>, que retorna o índice de base zero na instância de cadeia de caracteres atual da primeira ocorrência de qualquer caractere em uma matriz de caracteres.

- <xref:System.String.LastIndexOf%2A>, que retorna o índice de base zero da última ocorrência de um caractere ou uma cadeia de caracteres em uma instância de cadeia de caracteres.

- <xref:System.String.LastIndexOfAny%2A>, que retorna um índice de base zero na instância de cadeia de caracteres atual da última ocorrência de qualquer caractere em uma matriz de caracteres.

O exemplo a seguir usa o <xref:System.String.IndexOf%2A> método para localizar os períodos em uma cadeia de caracteres. Em seguida, ele usa o <xref:System.String.Substring%2A> método para retornar frases completas.

:::code language="csharp" source="snippets/parse-strings/csharp/indexof.cs" id="1" interactive="try-dotnet":::
:::code language="vb" source="snippets/parse-strings/vb/indexof.vb" id="1":::

## <a name="see-also"></a>Confira também

- [Operações básicas de cadeia de caracteres no .NET](basic-string-operations.md)
- [Expressões regulares do .NET](regular-expressions.md)
- [Como analisar cadeias de caracteres usando String. Split em C #](../../csharp/how-to/parse-strings-using-split.md)
