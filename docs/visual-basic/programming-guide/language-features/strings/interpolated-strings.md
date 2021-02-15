---
description: 'Saiba mais sobre: cadeias de caracteres interpoladas (referência de Visual Basic)'
title: Cadeias de caracteres interpoladas
ms.date: 10/31/2017
ms.openlocfilehash: c054401070079bdf85181619ef43c246feea5e18
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100429647"
---
# <a name="interpolated-strings-visual-basic-reference"></a>Cadeias de caracteres interpoladas (referência de Visual Basic)

Usado para construir cadeias de caracteres.  Uma cadeia de caracteres interpolada é semelhante a uma cadeia de caracteres de modelo que contém *expressões interpoladas*.  Uma cadeia de caracteres interpolada retorna uma cadeia de caracteres que substitui as expressões interpoladas que ela contém por suas representações de cadeia de caracteres. Esse recurso está disponível no Visual Basic 14 e versões posteriores.

Os argumentos de uma cadeia de caracteres interpolada são mais fáceis de entender do que uma [cadeia de caracteres de formato composto](../../../../standard/base-types/composite-formatting.md#composite-format-string).  Por exemplo, a cadeia de caracteres interpolada

```vb
Console.WriteLine($"Name = {name}, hours = {hours:hh}")
```

contém duas expressões interpoladas, "{name}" e "{hours:hh}". A cadeia de caracteres de formato composto equivalente é:

```vb
Console.WriteLine("Name = {0}, hours = {1:hh}", name, hours)
```

A estrutura de uma cadeia de caracteres interpolada é:

```vb
$"<text> {<interpolated-expression> [,<field-width>] [:<format-string>] } <text> ..."
```

em que:

- *field-width* é um inteiro com sinal que indica o número de caracteres no campo. Se ele for positivo, o campo será alinhado à direita. Se for negativo, será alinhado à esquerda.

- *format-string* é uma cadeia de caracteres de formato apropriada para o tipo do objeto que está sendo formatado. Por exemplo, para um <xref:System.DateTime> valor, pode ser uma [cadeia de caracteres de formato de data e hora padrão](../../../../standard/base-types/standard-date-and-time-format-strings.md) , como "d" ou "d".

> [!IMPORTANT]
> Você não pode ter nenhum espaço em branco entre o `$` e `"` que iniciam a cadeia de caracteres. Isso causa um erro do compilador.

Você pode usar uma cadeia de caracteres interpolada em qualquer lugar em que pode usar um literal de cadeia de caracteres.  A cadeia de caracteres interpolada é avaliada sempre que o código com a cadeia de caracteres interpolada for executado. Isso permite que você separe a definição e a avaliação de uma cadeia de caracteres interpolada.

Para incluir uma chave ("{" ou "}") em uma cadeia de caracteres interpolada, use duas chaves, "{{" ou "}}".  Consulte a seção sobre Conversões implícitas para obter mais detalhes.

Se a cadeia de caracteres interpolada contiver outros caracteres com significado especial em uma cadeia de caracteres interpolada, como aspas ("), dois-pontos (:) ou vírgulas (,), eles devem ser substituídos se ocorrerem no texto literal ou devem ser incluídos em uma expressão delimitada por parênteses se forem elementos de linguagem incluídos em uma expressão interpolada. O exemplo a seguir escapa as aspas para incluí-las na cadeia de caracteres de resultado:

[!code-vb[interpolated-strings](../../../../../samples/snippets/visualbasic/programming-guide/language-features/strings/interpolated-strings4.vb)]

## <a name="implicit-conversions"></a>Conversões implícitas

Há três conversões de tipo implícitas de uma cadeia de caracteres interpolada:

1. Conversão de uma cadeia de caracteres interpolada em um <xref:System.String>. O exemplo a seguir retorna uma cadeia de caracteres cujas expressões de cadeia de caracteres interpolada foram substituídas por suas representações de cadeia de caracteres. Por exemplo:

   [!code-vb[interpolated-strings1](../../../../../samples/snippets/visualbasic/programming-guide/language-features/strings/interpolated-strings1.vb)]

   Esse é o resultado final de uma interpretação de cadeia de caracteres. Todas as ocorrências de chaves duplas ("{{" e "}}") serão convertidas em uma chave única.

2. Conversão de uma cadeia de caracteres interpolada em uma variável <xref:System.IFormattable> que permite criar várias cadeias de caracteres de resultado com conteúdo específico da cultura de uma única instância <xref:System.IFormattable>. Isso é útil para incluir itens como os formatos de número e data corretos para culturas individuais.  Todas as ocorrências de chaves duplas ("{{" e "}}") permanecem como chaves duplas até que você formate a cadeia de caracteres explícita ou implicitamente chamando o método <xref:System.Object.ToString>.  Todas as expressões de interpolação contidas são convertidas em {0} , {1} e assim por diante.

   O exemplo a seguir usa reflexão para exibir os membros, bem como os valores de campo e propriedade de uma variável <xref:System.IFormattable> criada de uma cadeia de caracteres interpolada. Ele também passa a variável <xref:System.IFormattable> para o método <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType>.

   [!code-vb[interpolated-strings2](../../../../../samples/snippets/visualbasic/programming-guide/language-features/strings/interpolated-strings2.vb)]

   Observe que a cadeia de caracteres interpolada pode ser inspecionada somente usando a reflexão. Se ela for passada para um método de formatação de cadeia de caracteres, como <xref:System.Console.WriteLine(System.String)>, seus itens de formato serão resolvidos e a cadeia de caracteres de resultado será retornada.

3. Conversão de uma cadeia de caracteres interpolada em uma <xref:System.FormattableString> variável que representa uma cadeia de caracteres de formato composto. Inspecionar a cadeia de caracteres de formato composto e como ela é renderizada como uma cadeia de caracteres de resultado pode, por exemplo, ajudar a proteger contra um ataque de injeção se você estiver criando uma consulta. Um <xref:System.FormattableString> também inclui:

      - Uma sobrecarga <xref:System.FormattableString.ToString> que produza uma cadeia de caracteres de resultado para a <xref:System.Globalization.CultureInfo.CurrentCulture>.

      - Um <xref:System.FormattableString.Invariant%2A> método que produz uma cadeia de caracteres para o <xref:System.Globalization.CultureInfo.InvariantCulture> .

      - Um método <xref:System.FormattableString.ToString(System.IFormatProvider)> que produza uma cadeia de caracteres de resultado para uma cultura específica.

    Todas as ocorrências de chaves duplas ("{{" e "}}") permanecem como chaves duplas até que você formate.  Todas as expressões de interpolação contidas são convertidas em {0} , {1} e assim por diante.

   [!code-vb[interpolated-strings3](../../../../../samples/snippets/visualbasic/programming-guide/language-features/strings/interpolated-strings3.vb)]

## <a name="see-also"></a>Consulte também

- <xref:System.IFormattable?displayProperty=nameWithType>
- <xref:System.FormattableString?displayProperty=nameWithType>
- [Referência da linguagem Visual Basic](index.md)
