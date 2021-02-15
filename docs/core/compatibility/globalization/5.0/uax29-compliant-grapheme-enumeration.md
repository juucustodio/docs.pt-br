---
title: 'Alteração significativa: StringInfo e TextElementEnumerator agora são compatíveis com UAX29'
description: Saiba mais sobre a alteração significativa de globalização no .NET 5,0 em que StringInfo e TextElementEnumerator processam clusters grafemas de acordo com a versão mais recente do padrão Unicode.
ms.date: 04/07/2020
ms.openlocfilehash: cd5ae5a3eb9f2dd9c02bc179a40d454d24101199
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760324"
---
# <a name="stringinfo-and-textelementenumerator-are-now-uax29-compliant"></a>StringInfo e TextElementEnumerator agora são compatíveis com UAX29

Antes dessa alteração, <xref:System.Globalization.StringInfo?displayProperty=fullName> e <xref:System.Globalization.TextElementEnumerator?displayProperty=fullName> não tratamos adequadamente de todos os clusters do grafemas. Algumas graphemes foram divididas em seus componentes constituintes em vez de serem mantidas juntas. Agora, <xref:System.Globalization.StringInfo> e <xref:System.Globalization.TextElementEnumerator> processe os clusters grafemas de acordo com a versão mais recente do padrão Unicode.

Além disso, o <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName> método, que reverte os caracteres em uma cadeia de caracteres em Visual Basic, agora também segue o padrão Unicode para clusters grafemas.

## <a name="change-description"></a>Descrição das alterações

Um cluster [grafemas](https://www.unicode.org/glossary/#grapheme) ou [grafemas estendido](https://www.unicode.org/glossary/#extended_grapheme_cluster) é um único caractere percebido pelo usuário que pode ser composto por vários pontos de código Unicode. Por exemplo, a cadeia de caracteres que contém o caractere Tai "Kam" ( :::no-loc text="กำ"::: ) consiste nos dois caracteres a seguir:

- :::no-loc text="ก"::: (= ' \u0e01 ') CARACTERE TAI KO KAI
- :::no-loc text=" ำ"::: (= ' \u0e33 ') CARACTERE TAI SARA AM

Quando exibido para o usuário, o sistema operacional combina os dois caracteres para formar o único caractere de exibição (ou grafemas) "Kam" ou :::no-loc text="กำ"::: . O emoji também pode consistir em vários caracteres que são combinados para exibição de forma semelhante.

> [!TIP]
> A documentação do .NET às vezes usa o termo "elemento de texto" ao fazer referência a um grafemas.

As <xref:System.Globalization.StringInfo> <xref:System.Globalization.TextElementEnumerator> classes e inspecionam cadeias de caracteres e retornam informações sobre as graphemes que elas contêm. No .NET Framework (todas as versões) e no .NET Core 3. x e versões anteriores, essas duas classes usam lógica personalizada que lida com algumas classes combinadoras, mas que não está totalmente em conformidade com o [padrão Unicode](https://www.unicode.org/reports/tr29/tr29-35.html#Grapheme_Cluster_Boundaries). Por exemplo, as <xref:System.Globalization.StringInfo> <xref:System.Globalization.TextElementEnumerator> classes e dividem incorretamente o caractere Tai único "Kam" de volta em seus componentes constituintes em vez de mantê-los juntos. Essas classes também dividem incorretamente o caractere de Emoji "🤷🏽 ♀️" em quatro clusters (pessoa shrugging, modificador de Tom de pele, modificador de sexo e um combinador invisível) em vez de mantê-los juntos como um único cluster grafemas.

A partir do .NET 5, <xref:System.Globalization.StringInfo> as <xref:System.Globalization.TextElementEnumerator> classes e implementam o padrão Unicode conforme definido pelo [anexo 29 do padrão Unicode \# , Rev. 35, seg. 3](https://www.unicode.org/reports/tr29/tr29-35.html). Em particular, eles agora retornam [clusters grafemas estendidos](https://www.unicode.org/glossary/#extended_grapheme_cluster) para todas as classes combinadas.

Considere o seguinte código C#:

```csharp
using System.Globalization;

static void Main(string[] args)
{
    PrintGraphemes("กำ");
    PrintGraphemes("🤷🏽‍♀️");
}

static void PrintGraphemes(string str)
{
    Console.WriteLine($"Printing graphemes of \"{str}\"...");
    int i = 0;

    TextElementEnumerator enumerator = StringInfo.GetTextElementEnumerator(str);
    while (enumerator.MoveNext())
    {
        Console.WriteLine($"Grapheme {++i}: \"{enumerator.Current}\"");
    }

    Console.WriteLine($"({i} grapheme(s) total.)");
    Console.WriteLine();
}
```

No .NET Framework e no .NET Core 3. x e versões anteriores, os graphemes são divididos e a saída do console é a seguinte:

```txt
Printing graphemes of "กำ"...
Grapheme 1: "ก"
Grapheme 2: "ำ"
(2 grapheme(s) total.)

Printing graphemes of "🤷🏽‍♀️"...
Grapheme 1: "🤷"
Grapheme 2: "🏽"
Grapheme 3: "‍"
Grapheme 4: "♀️"
(4 grapheme(s) total.)
```

No .NET 5 e versões posteriores, os graphemes são mantidos juntos e a saída do console é a seguinte:

```txt
Printing graphemes of "กำ"...
Grapheme 1: "กำ"
(1 grapheme(s) total.)

Printing graphemes of "🤷🏽‍♀️"...
Grapheme 1: "🤷🏽‍♀️"
(1 grapheme(s) total.)
```

Além disso, a partir do .NET 5, o <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName> método, que reverte os caracteres em uma cadeia de caracteres em Visual Basic, agora também segue o padrão Unicode para clusters grafemas.

Essas alterações fazem parte de um conjunto mais amplo de aprimoramentos de Unicode e UTF-8 no .NET, incluindo uma API de enumeração de cluster grafemas estendida para complementar as APIs de enumeração de valor escalar Unicode que foram introduzidas com o <xref:System.Text.Rune?displayProperty=fullName> tipo no .NET Core 3,0.

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

Você não precisa realizar nenhuma ação. Seus aplicativos se comportarão automaticamente em uma maneira mais compatível com padrões em uma variedade de cenários relacionados à globalização.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Globalization.StringInfo?displayProperty=fullName>
- <xref:System.Globalization.TextElementEnumerator?displayProperty=fullName>
- <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName>

<!--

### Affected APIs

- `T:System.Globalization.StringInfo`
- `T:System.Globalization.TextElementEnumerator`
- `Overload:Microsoft.VisualBasic.Strings.StrReverse`

### Category

Globalization

-->
