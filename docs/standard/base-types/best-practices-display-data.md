---
title: Práticas recomendadas para exibir e persistir dados formatados no .NET
description: Saiba como exibir e manter dados numéricos e de data efetivamente em aplicativos .NET.
ms.date: 05/01/2019
ms.topic: conceptual
dev_langs:
- csharp
- vb
ms.openlocfilehash: dd2e85ed695072da24b6b25b187810a109b89b25
ms.sourcegitcommit: 4313614f57690f9a5119a37314f0a1fd738ebda2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2021
ms.locfileid: "98693118"
---
# <a name="best-practices-for-displaying-and-persisting-formatted-data"></a>Práticas recomendadas para exibir e manter dados formatados

Este artigo examina como os dados formatados, como dados numéricos e dados de data e hora, são tratados para exibição e armazenamento.

Ao desenvolver com o .NET, use a formatação sensível à cultura para exibir dados que não são de cadeia de caracteres, como números e datas, em uma interface do usuário. Use a formatação com a [cultura invariável](xref:System.Globalization.CultureInfo.InvariantCulture) para persistir os dados que não são de cadeias de caracteres no formato de cadeia de caracteres. Não use formatação sensível à cultura para manter dados numéricos ou de data e hora no formato de cadeia de caracteres.

## <a name="displaying-formatted-data"></a>Exibindo dados formatados

Quando você exibir dados que não são de cadeias de caracteres como números e datas e horas para os usuários, formate-os usando as configurações culturais do usuário. Por padrão, todos itens a seguir usam a cultura do thread atual em operações de formatação:

- Cadeias de caracteres interpoladas compatíveis com os compiladores [C#](../../csharp/language-reference/tokens/interpolated.md) e [Visual Basic](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md).
- Operações de concatenação de cadeias de caracteres que usam os operadores de concatenação do [C#](../../csharp/language-reference/operators/addition-operator.md#string-concatenation) ou [Visual Basic](../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md), ou que chamam o método <xref:System.String.Concat%2A?displayProperty=nameWithType> diretamente.
- O método <xref:System.String.Format%2A?displayProperty=nameWithType>.
- Os métodos `ToString` dos tipos numéricos e dos tipos de data e hora.

Para especificar explicitamente que uma cadeia de caracteres deve ser formatada usando as convenções de uma cultura específica ou a [cultura invariável](xref:System.Globalization.CultureInfo.InvariantCulture), você pode fazer o seguinte:

- Ao usar os métodos <xref:System.String.Format%2A?displayProperty=nameWithType> e `ToString`, chame uma sobrecarga que tenha um parâmetro `provider`, tal como <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> ou <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=nameWithType>, e passe a ela a propriedade <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>, a propriedade <xref:System.Globalization.CultureInfo.InvariantCulture?displayProperty=nameWithType> ou uma instância de <xref:System.Globalization.CultureInfo> que represente a cultura desejada.

- Para concatenação de cadeias de caracteres, não permita que o compilador execute nenhuma conversão implícita. Em vez disso, execute uma conversão explícita, chamando uma sobrecarga `ToString` que tenha um parâmetro `provider`. Por exemplo, o compilador usa implicitamente a cultura atual ao converter um <xref:System.Double> valor em uma cadeia de caracteres no código a seguir:

  [!code-csharp[Implicit String Conversion](./snippets/best-practices-strings/csharp/tostring/Program.cs#1)]
  [!code-vb[Implicit String Conversion](./snippets/best-practices-strings/vb/tostring/Program.vb#1)]

  Em vez disso, você pode especificar explicitamente a cultura cujas convenções de formatação são usadas na conversão chamando o <xref:System.Double.ToString(System.IFormatProvider)?displayProperty=nameWithType> método, como o código a seguir:

  [!code-csharp[Explicit String Conversion](./snippets/best-practices-strings/csharp/tostring/Program.cs#2)]
  [!code-vb[Implicit String Conversion](./snippets/best-practices-strings/vb/tostring/Program.vb#2)]

- Para a interpolação de cadeia de caracteres, em vez de atribuir uma cadeia de caracteres interpolada a uma instância de <xref:System.String>, atribua-a a um <xref:System.FormattableString>. Em seguida, você pode chamar o respectivo método <xref:System.FormattableString.ToString?displayProperty=nameWithType> para produzir uma cadeia de caracteres de resultado que reflete as convenções da cultura atual, ou então pode chamar o método <xref:System.FormattableString.ToString(System.IFormatProvider)?displayProperty=nameWithType> para produzir uma cadeia de caracteres de resultado que reflete as convenções de uma cultura específica. Você também pode passar a cadeia de caracteres formatável para o método <xref:System.FormattableString.Invariant%2A?displayProperty=nameWithType> estático para produzir uma cadeia de caracteres de resultado que reflete as convenções da cultura invariável. O exemplo a seguir ilustra esta abordagem. (A saída do exemplo reflete uma cultura atual de en-US.)

  [!code-csharp[String interpolation](./snippets/best-practices-strings/csharp/formattable/Program.cs)]
  [!code-vb[String interpolation](./snippets/best-practices-strings/vb/formattable/Program.vb)]

## <a name="persisting-formatted-data"></a>Mantendo dados formatados

Você pode manter os dados que não são de cadeias de caracteres como dados binários ou como dados formatados. Se optar por salvá-los como dados formatados, você deverá chamar uma sobrecarga de método de formatação que inclua um parâmetro `provider` e passar para ele a propriedade <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>. A cultura invariável fornece um formato consistente para os dados formatados que é independente da cultura e do computador. Em contraste, dados persistentes que são formatados usando culturas diferentes da cultura invariável têm várias limitações:

- É provável que os dados não sejam utilizáveis se forem recuperados em um sistema que tem uma cultura diferente ou se o usuário do sistema atual alterar a cultura atual e tentar recuperar os dados.
- As propriedades de uma cultura em um computador específico podem ser diferentes dos valores padrão. A qualquer momento, um usuário pode personalizar as configurações de exibição que levam em conta a cultura. Devido a isso, os dados formatados que são salvos em um sistema podem não ser legíveis após o usuário personalizar as configurações culturais. É provável que a portabilidade dos dados formatados entre computadores seja ainda mais limitada.
- Os padrões internacionais, regionais ou nacionais que controlam a formatação de números ou datas e horas são alterados ao longo do tempo e essas alterações são incorporadas nas atualizações do sistema operacional Windows. Quando as convenções de formatação mudam, os dados que foram formatados usando as convenções anteriores podem se tornar ilegíveis.

O exemplo a seguir ilustra a portabilidade limitada resultante do uso da formatação que leva em conta a cultura para manter os dados. O exemplo salva uma matriz de valores de data e hora em um arquivo. Eles são formatados usando as convenções da cultura do inglês (Estados Unidos). Depois que o aplicativo altera a cultura do thread atual para francês (Suíça), ele tenta ler os valores salvos usando as convenções de formatação da cultura atual. A tentativa de ler dois dos itens de dados gera uma exceção <xref:System.FormatException> e a matriz de datas agora contém dois elementos incorretos que são iguais a <xref:System.DateTime.MinValue>.

[!code-csharp[Conceptual.Strings.BestPractices#21](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/persistence.cs#21)]
[!code-vb[Conceptual.Strings.BestPractices#21](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/persistence.vb#21)]

No entanto, se você substituir a <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> Propriedade por <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> nas chamadas para <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> e <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> , os dados persistentes de data e hora serão restaurados com êxito, como mostra a seguinte saída:

```console
06.05.1758 21:26
05.05.1818 07:19
22.04.1870 23:54
08.09.1890 06:47
18.02.1905 15:12
```
