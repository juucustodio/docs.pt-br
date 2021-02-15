---
title: Como converter uma cadeia de caracteres em um guia de programação de um número C#
description: Saiba como converter uma cadeia de caracteres em um número em C# chamando os métodos de classe Parse, TryParse ou Convert.
ms.date: 11/20/2020
helpviewer_keywords:
- conversions [C#]
- conversions [C#], string to int
- converting strings to int [C#]
- strings [C#], converting to int
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 467b9979-86ee-4afd-b734-30299cda91e3
ms.openlocfilehash: 430887ebb16570439a89f3625ac12a1fbb368227
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513153"
---
# <a name="how-to-convert-a-string-to-a-number-c-programming-guide"></a>Como converter uma cadeia de caracteres em um número (guia de programação C#)

Você pode converter uma [cadeia de caracteres](../../language-reference/builtin-types/reference-types.md) em um número chamando `Parse` o `TryParse` método ou encontrado nos vários tipos numéricos ( `int` ,, `long` `double` e assim por diante) ou usando métodos na <xref:System.Convert?displayProperty=nameWithType> classe.  
  
 É um pouco mais eficiente e direto chamar um `TryParse` método (por exemplo, [`int.TryParse("11", out number)`](xref:System.Int32.TryParse%2A) ) ou `Parse` método (por exemplo, [`var number = int.Parse("11")`](xref:System.Int32.Parse%2A) ).  Usar um método <xref:System.Convert> é mais útil para objetos gerais que implementam <xref:System.IConvertible>.  
  
 Você usa `Parse` `TryParse` métodos ou no tipo numérico que espera que a cadeia de caracteres contenha, como o <xref:System.Int32?displayProperty=nameWithType> tipo.  O método <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType> usa <xref:System.Int32.Parse%2A> internamente.  O `Parse` método retorna o número convertido; o `TryParse` método retorna um <xref:System.Boolean> valor que indica se a conversão foi bem-sucedida e retorna o número convertido em um [ `out` parâmetro](../../language-reference/keywords/out.md). Se a cadeia de caracteres não estiver em um formato válido, o `Parse` lançará uma exceção, mas `TryParse` retornará `false` . Ao chamar um método `Parse`, você sempre deve usar o tratamento de exceções para capturar um <xref:System.FormatException> no caso da operação de análise falhar.  
  
## <a name="calling-the-parse-and-tryparse-methods"></a>Como chamar os métodos Parse e TryParse

Os `Parse` `TryParse` métodos e ignoram o espaço em branco no início e no final da cadeia de caracteres, mas todos os outros caracteres devem ser caracteres que formam o tipo numérico apropriado (,,,, `int` `long` `ulong` `float` `decimal` e assim por diante).  Qualquer espaço em branco na cadeia de caracteres que forma o número causa um erro.  Por exemplo, você pode usar `decimal.TryParse` para analisar "10", "10,3" ou "10", mas não pode usar esse método para analisar 10 de "10x", "1 0" (Observe o espaço incorporado), "10 3" (Observe o espaço incorporado), "10e1" ( `float.TryParse` funciona aqui) e assim por diante. Uma cadeia de caracteres cujo valor é `null` ou não é possível <xref:System.String.Empty?displayProperty=nameWithType> analisar com êxito. Você pode verificar uma cadeia de caracteres nula ou vazia antes de tentar analisá-la chamando o método <xref:System.String.IsNullOrEmpty%2A?displayProperty=nameWithType>.

O exemplo a seguir demonstra chamadas com e sem êxito para `Parse` e `TryParse`.  
  
[!code-csharp[Parse and TryParse](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse/program.cs)]  

O exemplo a seguir ilustra uma abordagem para analisar uma cadeia de caracteres esperada para incluir caracteres numéricos à esquerda (incluindo caracteres hexadecimais) e caracteres não numéricos à direita. Ele atribui caracteres válidos do início de uma cadeia de caracteres até uma nova cadeia de caracteres antes de chamar o método <xref:System.Int32.TryParse%2A>. Como as cadeias de caracteres a ser analisadas contêm um pequeno número de caracteres, o exemplo chama o método <xref:System.String.Concat%2A?displayProperty=nameWithType> para atribuir os caracteres válidos em uma nova cadeia de caracteres. Para cadeias de caracteres maiores, pode ser usada a classe <xref:System.Text.StringBuilder>.
  
[!code-csharp[Removing invalid characters](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse2/program.cs)]  

## <a name="calling-the-convert-methods"></a>Chamar os métodos de conversão

A tabela a seguir lista alguns dos métodos da classe <xref:System.Convert> que podem ser usados para converter uma cadeia de caracteres em um número.  
  
|Tipo numérico|Método|  
|------------------|------------|  
|`decimal`|<xref:System.Convert.ToDecimal%28System.String%29>|  
|`float`|<xref:System.Convert.ToSingle%28System.String%29>|  
|`double`|<xref:System.Convert.ToDouble%28System.String%29>|  
|`short`|<xref:System.Convert.ToInt16%28System.String%29>|  
|`int`|<xref:System.Convert.ToInt32%28System.String%29>|  
|`long`|<xref:System.Convert.ToInt64%28System.String%29>|  
|`ushort`|<xref:System.Convert.ToUInt16%28System.String%29>|  
|`uint`|<xref:System.Convert.ToUInt32%28System.String%29>|  
|`ulong`|<xref:System.Convert.ToUInt64%28System.String%29>|  
  
 O exemplo a seguir chama o <xref:System.Convert.ToInt32%28System.String%29?displayProperty=nameWithType> método para converter uma cadeia de caracteres de entrada em um [int](../../language-reference/builtin-types/integral-numeric-types.md). O exemplo captura as duas exceções mais comuns que podem ser geradas por esse método <xref:System.FormatException> e <xref:System.OverflowException> . Se o número resultante puder ser incrementado sem exceder <xref:System.Int32.MaxValue?displayProperty=nameWithType>, o exemplo adicionará 1 ao resultado e exibirá a saída.  
  
[!code-csharp[Parsing with Convert methods](~/samples/snippets/csharp/programming-guide/string-to-number/convert/program.cs)]  
  
## <a name="see-also"></a>Consulte também

- [Types](./index.md)
- [Como determinar se uma cadeia de caracteres representa um valor numérico](../strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)
- [Amostra: Utilitário de Formatação do WinForms do .NET Core (C#)](/samples/dotnet/samples/windowsforms-formatting-utility-cs)
