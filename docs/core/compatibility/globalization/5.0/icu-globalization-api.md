---
title: 'Alteração significativa: as APIs de globalização usam bibliotecas ICU no Windows'
description: Saiba mais sobre a alteração significativa de globalização no .NET 5,0 em que as bibliotecas ICU são usadas para a funcionalidade de globalização em vez do NLS.
ms.date: 05/19/2020
ms.openlocfilehash: efc20e21969ea4a83c9122e40b262e1dc38e6770
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760539"
---
# <a name="globalization-apis-use-icu-libraries-on-windows"></a>APIs de globalização usam bibliotecas ICU no Windows

O .NET 5,0 e versões posteriores usam bibliotecas [internacionais para](http://site.icu-project.org/home) a funcionalidade de globalização na execução no Windows 10 pode ser 2019 atualização ou posterior.

## <a name="change-description"></a>Descrição das alterações

No .NET Core 1,0-3,1 e .NET Framework 4 e versões posteriores, as bibliotecas do .NET usam APIs [NLS (suporte a idioma nacional)](/windows/win32/intl/national-language-support) para a funcionalidade de globalização no Windows. Por exemplo, as funções NLS foram usadas para comparar cadeias de caracteres, obter informações de cultura e executar maiúsculas e minúsculas na cultura apropriada.

A partir do .NET 5,0, se um aplicativo estiver em execução no Windows 10 pode ser 2019 Update ou posterior, as bibliotecas do .NET usarão APIs de globalização [ICU](http://site.icu-project.org/home) , por padrão.

> [!NOTE]
> O Windows 10 pode 2019 atualização e versões posteriores são fornecidas com a biblioteca nativa do ICU. Se o tempo de execução do .NET não puder carregar o ICU, ele usará o NLS.

## <a name="behavioral-differences"></a>Diferenças de comportamento

Você poderá ver as alterações em seu aplicativo mesmo se não perceber que está usando instalações de globalização. Esta seção lista algumas das alterações comportamentais que você pode ver, mas também há outras.

### <a name="stringindexof"></a>String.IndexOf

Considere o código a seguir que chama <xref:System.String.IndexOf(System.String)?displayProperty=nameWithType> para localizar o índice do caractere de nova linha em uma cadeia de caracteres.

```csharp
string s = "Hello\r\nworld!";
int idx = s.IndexOf("\n");
Console.WriteLine(idx);
```

- Nas versões anteriores do .NET no Windows, o trecho é impresso `6` .
- No .NET 5,0 e versões posteriores no Windows 19H1 e versões posteriores, o trecho de código é impresso `-1` .

Para corrigir esse código realizando uma pesquisa ordinal em vez de uma pesquisa sensível à cultura, chame a <xref:System.String.IndexOf(System.String,System.StringComparison)> sobrecarga e passe <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> como um argumento.

Você pode executar as regras [de análise de código CA1307: especificar StringComparison para clareza](../../../../fundamentals/code-analysis/quality-rules/ca1307.md) e [CA1309: Use o ordinal StringComparison](../../../../fundamentals/code-analysis/quality-rules/ca1309.md) para encontrar esses sites de chamada em seu código.

Para obter mais informações, consulte [comportamento de alterações ao comparar cadeias de caracteres no .NET 5 +](../../../../standard/base-types/string-comparison-net-5-plus.md).

### <a name="currency-symbol"></a>Símbolo de moeda

Considere o código a seguir que formata uma cadeia de caracteres usando o especificador de formato de moeda `C` . A cultura do thread atual é definida como uma cultura que inclui apenas o idioma e não o país.

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("de");
string text = string.Format("{0:C}", 100);
```

- Nas versões anteriores do .NET no Windows, o valor do texto é `"100,00 €"` .
- No .NET 5,0 e versões posteriores no Windows 19H1 e versões posteriores, o valor de Text é `"100,00 ¤"` , que usa o símbolo de moeda internacional em vez do euro. No ICU, o design é que uma moeda é uma propriedade de um país ou região, não um idioma.

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi introduzida para unificar. Comportamento de globalização da rede em todos os sistemas operacionais com suporte. Ele também fornece a capacidade de os aplicativos agruparem suas próprias bibliotecas de globalização em vez de depender das bibliotecas internas do sistema operacional.

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

Nenhuma ação é necessária na parte do desenvolvedor. No entanto, se você quiser continuar usando as APIs de globalização NLS, poderá definir uma [opção de tempo de execução](../../../run-time-config/globalization.md#nls) para reverter para esse comportamento. Para obter mais informações sobre as opções disponíveis, consulte o artigo [globalização .net e ICU](../../../../standard/globalization-localization/globalization-icu.md) .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Span%601?displayProperty=fullName>
- <xref:System.String?displayProperty=fullName>
- Maioria dos tipos no <xref:System.Globalization?displayProperty=fullName> namespace
- <xref:System.Array.Sort%2A?displayProperty=fullName> (ao classificar uma matriz de cadeias de caracteres)
- <xref:System.Collections.Generic.List%601.Sort?displayProperty=fullName> (quando os elementos da lista são cadeias de caracteres)
- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName> (quando as chaves são cadeias de caracteres)
- <xref:System.Collections.Generic.SortedList%602?displayProperty=fullName> (quando as chaves são cadeias de caracteres)
- <xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName> (quando o conjunto contém cadeias de caracteres)

<!--

### Affected APIs

- ``T:System.Span`1``
- `T:System.String`
- `N:System.Globalization`
- `Overload:System.Array.Sort`
- ``M:System.Collections.Generic.List`1.Sort``
- ``T:System.Collections.Generic.SortedDictionary`2``
- ``T:System.Collections.Generic.SortedList`2``
- ``T:System.Collections.Generic.SortedSet`1``

### Category

- Core .NET libraries
- Globalization

-->
