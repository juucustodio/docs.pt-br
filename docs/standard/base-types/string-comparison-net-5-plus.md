---
title: Alterações de comportamento ao comparar cadeias de caracteres no .NET 5 +
description: Saiba mais sobre alterações de comportamento de comparação de cadeia de caracteres no .NET 5 e versões posteriores no Windows.
ms.date: 12/07/2020
ms.openlocfilehash: a53c36b31785fb43c0aa5f5040042abb6d40031a
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851745"
---
# <a name="behavior-changes-when-comparing-strings-on-net-5"></a>Alterações de comportamento ao comparar cadeias de caracteres no .NET 5 +

O .NET 5,0 apresenta uma alteração comportamental de tempo de execução em que as APIs de globalização [agora usam o ICU por padrão](../../core/compatibility/globalization/5.0/icu-globalization-api.md) em todas as plataformas com suporte. Essa é uma partida de versões anteriores do .NET Core e da .NET Framework, que utiliza a funcionalidade NLS (suporte ao idioma nacional) do sistema operacional quando executada no Windows. Para obter mais informações sobre essas alterações, incluindo opções de compatibilidade que podem reverter a alteração de comportamento, consulte [.net Globalization and ICU](../globalization-localization/globalization-icu.md).

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi introduzida para unificar. Comportamento de globalização da rede em todos os sistemas operacionais com suporte. Ele também fornece a capacidade de os aplicativos agruparem suas próprias bibliotecas de globalização em vez de depender das bibliotecas internas do sistema operacional. Para obter mais informações, confira [a notificação de alteração interruptiva](../../core/compatibility/globalization/5.0/icu-globalization-api.md).

## <a name="behavioral-differences"></a>Diferenças de comportamento

Se você usar funções como `string.IndexOf(string)` sem chamar a sobrecarga que usa um <xref:System.StringComparison> argumento, Talvez pretenda executar uma pesquisa *ordinal* , mas, em vez disso, você assume inadvertidamente uma dependência do comportamento específico da cultura. Como NLS e ICU implementam lógicas diferentes em seus comparadores lingüísticos, os resultados de métodos como `string.IndexOf(string)` podem retornar valores inesperados.

Isso pode se manifestar mesmo em locais onde você nem sempre está esperando que as instalações de globalização estejam ativas. Por exemplo, o código a seguir pode produzir uma resposta diferente dependendo do tempo de execução atual.

```cs
string s = "Hello\r\nworld!";
int idx = s.IndexOf("\n");
Console.WriteLine(idx);

// The snippet prints:
//
// '6' when running on .NET Framework (Windows)
// '6' when running on .NET Core 2.x - 3.x (Windows)
// '-1' when running on .NET 5 (Windows)
// '-1' when running on .NET Core 2.x - 3.x or .NET 5 (non-Windows)
// '6' when running on .NET Core 2.x or .NET 5 (in invariant mode)
```

## <a name="guard-against-unexpected-behavior"></a>Proteção contra comportamento inesperado

Esta seção fornece duas opções para lidar com alterações de comportamento inesperadas no .NET 5,0.

### <a name="enable-code-analyzers"></a>Habilitar analisadores de código

[Analisadores de código](../../fundamentals/code-analysis/overview.md) podem detectar sites de chamada possivelmente com bugs. Para ajudar a proteger contra qualquer comportamento surpreendente, recomendamos habilitar os analisadores de Roslyn (plataforma de compilador .NET) em seu projeto. Os analisadores ajudam a codificar o código que pode usar inadvertidamente um comparador lingüístico quando um comparador ordinal era provavelmente pretendido. As regras a seguir devem ajudar a sinalizar esses problemas:

- [CA1307: Especificar StringComparison para garantir a clareza](../../fundamentals/code-analysis/quality-rules/ca1307.md)
- [CA1309: Usar StringComparison ordinal](../../fundamentals/code-analysis/quality-rules/ca1309.md)
- [CA1310: Especificar StringComparison para garantir a exatidão](../../fundamentals/code-analysis/quality-rules/ca1310.md)

Essas regras específicas não são habilitadas por padrão. Para habilitá-los e mostrar quaisquer violações como erros de compilação, defina as seguintes propriedades em seu arquivo de projeto:

```xml
<PropertyGroup>
  <AnalysisMode>AllEnabledByDefault</AnalysisMode>
  <WarningsAsErrors>$(WarningsAsErrors);CA1307;CA1309;CA1310</WarningsAsErrors>
</PropertyGroup>
```

O trecho a seguir mostra exemplos de código que produz os avisos ou erros relevantes do analisador de código.

```cs
//
// Potentially incorrect code - answer might vary based on locale.
//
string s = GetString();
// Produces analyzer warning CA1310 for string; CA1307 matches on char ','
int idx = s.IndexOf(",");
Console.WriteLine(idx);

//
// Corrected code - matches the literal substring ",".
//
string s = GetString();
int idx = s.IndexOf(",", StringComparison.Ordinal);
Console.WriteLine(idx);

//
// Corrected code (alternative) - searches for the literal ',' character.
//
string s = GetString();
int idx = s.IndexOf(',');
Console.WriteLine(idx);
```

Da mesma forma, ao criar uma instância de uma coleção classificada de cadeias de caracteres ou classificar uma coleção baseada em cadeia existente, especifique um comparador explícito.

```cs
//
// Potentially incorrect code - behavior might vary based on locale.
//
SortedSet<string> mySet = new SortedSet<string>();
List<string> list = GetListOfStrings();
list.Sort();

//
// Corrected code - uses ordinal sorting; doesn't vary by locale.
//
SortedSet<string> mySet = new SortedSet<string>(StringComparer.Ordinal);
List<string> list = GetListOfStrings();
list.Sort(StringComparer.Ordinal);
```

### <a name="revert-back-to-nls-behaviors"></a>Reverter para os comportamentos NLS

Para reverter os aplicativos do .NET 5 para os comportamentos NLS mais antigos ao executar no Windows, siga as etapas em [.net Globalization e ICU](../globalization-localization/globalization-icu.md). Essa opção de compatibilidade em todo o aplicativo deve ser definida no nível do aplicativo. Bibliotecas individuais não podem aceitar ou recusar esse comportamento.

> [!TIP]
> É altamente recomendável que você habilite as regras de análise de código [CA1307](../../fundamentals/code-analysis/quality-rules/ca1307.md), [CA1309](../../fundamentals/code-analysis/quality-rules/ca1309.md)e [CA1310](../../fundamentals/code-analysis/quality-rules/ca1310.md) para ajudar a melhorar a higienização de código e descobrir quaisquer bugs latentes existentes. Para obter mais informações, consulte [habilitar analisadores de código](#enable-code-analyzers).

## <a name="affected-apis"></a>APIs afetadas

A maioria dos aplicativos .NET não encontrará comportamentos inesperados devido às alterações no .NET 5,0. No entanto, devido ao número de APIs afetadas e à forma como as bases dessas APIs são para o ecossistema mais amplo do .NET, você deve estar ciente do potencial para que o .NET 5,0 Introduza comportamentos indesejados ou expor bugs latentes que já existem em seu aplicativo.

As APIs afetadas incluem:

- <xref:System.String.Compare%2A?displayProperty=fullName>
- <xref:System.String.EndsWith%2A?displayProperty=fullName>
- <xref:System.String.IndexOf%2A?displayProperty=fullName>
- <xref:System.String.StartsWith%2A?displayProperty=fullName>
- <xref:System.String.ToLower%2A?displayProperty=fullName>
- <xref:System.String.ToLowerInvariant%2A?displayProperty=fullName>
- <xref:System.String.ToUpper%2A?displayProperty=fullName>
- <xref:System.String.ToUpperInvariant%2A?displayProperty=fullName>
- <xref:System.Globalization.TextInfo?displayProperty=fullName> (a maioria dos membros)
- <xref:System.Globalization.CompareInfo?displayProperty=fullName> (a maioria dos membros)
- <xref:System.Array.Sort%2A?displayProperty=fullName> (ao classificar matrizes de cadeias de caracteres)
- <xref:System.Collections.Generic.List%601.Sort?displayProperty=fullName> (quando os elementos da lista são cadeias de caracteres)
- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName> (quando as chaves são cadeias de caracteres)
- <xref:System.Collections.Generic.SortedList%602?displayProperty=fullName> (quando as chaves são cadeias de caracteres)
- <xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName> (quando o conjunto contém cadeias de caracteres)

> [!NOTE]
> Esta não é uma lista completa de APIs afetadas.

Todas as APIs acima usam a pesquisa de cadeia de caracteres *linguística* e a comparação usando a [cultura atual](xref:System.Threading.Thread.CurrentCulture)do thread, por padrão. As diferenças entre a pesquisa *lingüística* e a *ordinal* e a comparação são chamadas na [pesquisa e comparação de ordinais e linguísticas](#ordinal-vs-linguistic-search-and-comparison).

Como o ICU implementa comparações lingüísticas de cadeias de caracteres de forma diferente de NLS, os aplicativos baseados no Windows que são atualizados para o .NET 5,0 de uma versão anterior do .NET Core ou .NET Framework e que chamam uma das APIs afetadas podem notar que as APIs começam a apresentar comportamentos diferentes.

### <a name="exceptions"></a>Exceções

* Se uma API aceitar um `StringComparison` parâmetro ou explícito `CultureInfo` , esse parâmetro substituirá o comportamento padrão da API.
* `System.String` os membros em que o primeiro parâmetro é do tipo `char` (por exemplo, <xref:System.String.IndexOf(System.Char)?displayProperty=nameWithType> ) usam a pesquisa ordinal, a menos que o chamador passe um `StringComparison` argumento explícito que especifica `CurrentCulture[IgnoreCase]` ou `InvariantCulture[IgnoreCase]` .

Para obter uma análise mais detalhada do comportamento padrão de cada <xref:System.String> API, consulte a seção [padrão pesquisa e tipos de comparação](#default-search-and-comparison-types) .

## <a name="ordinal-vs-linguistic-search-and-comparison"></a>Pesquisa e comparação de ordinal vs. linguística

A pesquisa e a comparação de *ordinal* (também conhecida como *não lingüística*) decompõem uma cadeia de caracteres em seus `char` elementos individuais e executa uma pesquisa Char-por-char ou uma comparação. Por exemplo, as cadeias de caracteres `"dog"` e `"dog"` comparar como *iguais* em um comparador `Ordinal` , já que as duas cadeias de caracteres consistem na mesma sequência exata de caracteres. No entanto, `"dog"` e `"Dog"` comparar como *não igual* em um comparador `Ordinal` , porque eles não consistem na mesma sequência exata de caracteres. Ou seja, o `'D'` ponto de código de maiúsculas `U+0044` ocorre antes `'d'` do ponto de código de minúsculas `U+0064` , resultando na `"dog"` classificação antes `"Dog"` .

Um comparador `OrdinalIgnoreCase` ainda opera com base Char-por-Char, mas elimina diferenças de maiúsculas e minúsculas ao executar a operação. Em um `OrdinalIgnoreCase` comparador, os pares de caracteres `'d'` e `'D'` comparar como *iguais*, assim como os pares de caracteres `'á'` e `'Á'` . Mas o caractere não acentuado `'a'` compara como *não igual* ao caractere acentuado `'á'` .

Alguns exemplos disso são fornecidos na tabela a seguir:

| Cadeia de caracteres 1 | Cadeia de caracteres 2 | `Ordinal` comparação | `OrdinalIgnoreCase` comparação |
|---|---|---|---|
| `"dog"` | `"dog"` | equal | equal |
| `"dog"` | `"Dog"` | diferente de | equal |
| `"resume"` | `"Resume"` | diferente de | equal |
| `"resume"` | `"résumé"` | diferente de | diferente de |

O Unicode também permite que as cadeias de caracteres tenham várias representações na memória diferentes. Por exemplo, um e-agudo (é) pode ser representado de duas maneiras possíveis:

* Um único `'é'` caractere literal (também escrito como `'\u00E9'` ).
* Um caractere literal não acentuado `'e'` , seguido por um caractere de modificador de acentuação de acento `'\u0301'` .

Isso significa que todas as _quatro_ cadeias de caracteres a seguir resultam em `"résumé"` quando exibidas, embora suas partes constituintes sejam diferentes. As strings usam uma combinação de caracteres literais `'é'` ou caracteres literais não acentuados, `'e'` além do modificador de acentuação combinável `'\u0301'` .

* `"r\u00E9sum\u00E9"`
* `"r\u00E9sume\u0301"`
* `"re\u0301sum\u00E9"`
* `"re\u0301sume\u0301"`

Em um comparador ordinal, nenhuma dessas cadeias de caracteres é comparada como igual uma da outra. Isso ocorre porque todos contêm sequências de caracteres subjacentes diferentes, mesmo quando são renderizados na tela, todos têm a mesma aparência.

Ao executar uma `string.IndexOf(..., StringComparison.Ordinal)` operação, o tempo de execução procura uma correspondência exata de subcadeia de caracteres. Os resultados são os seguintes.

```cs
Console.WriteLine("resume".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e", StringComparison.Ordinal)); // prints '-1'
Console.WriteLine("r\u00E9sume\u0301".IndexOf("e", StringComparison.Ordinal)); // prints '5'
Console.WriteLine("re\u0301sum\u00E9".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("re\u0301sume\u0301".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("resume".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '-1'
Console.WriteLine("r\u00E9sume\u0301".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '5'
Console.WriteLine("re\u0301sum\u00E9".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
Console.WriteLine("re\u0301sume\u0301".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
```

As rotinas de pesquisa e de comparação ordinais nunca são afetadas pela configuração de cultura do thread atual.

As rotinas de pesquisa e de comparação *linguística* decompõem uma cadeia de caracteres em *elementos de agrupamento* e realizam pesquisas ou comparações nesses elementos. Não há necessariamente um mapeamento 1:1 entre os caracteres de uma cadeia e seus elementos de agrupamento constituintes. Por exemplo, uma cadeia de caracteres de comprimento 2 pode consistir apenas de um único elemento de agrupamento. Quando duas cadeias de caracteres são comparadas de forma linguística, o comparador verifica se os elementos de agrupamento das duas cadeias de caracteres têm o mesmo significado semântico, mesmo que os caracteres literais da cadeia sejam diferentes.

Considere novamente a cadeia de caracteres `"résumé"` e suas quatro representações diferentes. A tabela a seguir mostra cada representação dividida em seus elementos de agrupamento.

| String | Como elementos de agrupamento |
|---|---|
| `"r\u00E9sum\u00E9"` | `"r" + "\u00E9" + "s" + "u" + "m" + "\u00E9"` |
| `"r\u00E9sume\u0301"` | `"r" + "\u00E9" + "s" + "u" + "m" + "e\u0301"` |
| `"re\u0301sum\u00E9"` | `"r" + "e\u0301" + "s" + "u" + "m" + "\u00E9"` |
| `"re\u0301sume\u0301"` | `"r" + "e\u00E9" + "s" + "u" + "m" + "e\u0301"` |

Um elemento de agrupamento corresponde livremente ao que os leitores consideram como um único caractere ou cluster de caracteres. Ele é conceitualmente semelhante a um [cluster grafemas](character-encoding-introduction.md#grapheme-clusters) , mas abrange uma proteção um pouco maior.

Em um comparador linguístico, as correspondências exatas não são necessárias. Em vez disso, os elementos de agrupamento são comparados com base no significado semântico. Por exemplo, um comparador linguístico trata as subcadeias de caracteres `"\u00E9"` e `"e\u0301"` como iguais, uma vez que ambas significam semanticamente "um e minúsculo com um modificador de acentos agudos". Isso permite que o `IndexOf` método coincida com a subcadeia de caracteres `"e\u0301"` em uma cadeia de caracteres maior que contém a subcadeia de caracteres semanticamente equivalente `"\u00E9"` , como mostrado no exemplo de código a seguir.

```cs
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e")); // prints '-1' (not found)
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e\u00E9")); // prints '1'
Console.WriteLine("\u00E9".IndexOf("e\u00E9")); // prints '0'
```

Como consequência disso, duas cadeias de caracteres de comprimentos diferentes podem ser comparadas como iguais se uma comparação linguística for usada. Os chamadores devem tomar cuidado para não ser uma lógica de caso especial que lida com o comprimento da cadeia de caracteres nesses cenários.

As rotinas de comparação e pesquisa *com reconhecimento de cultura* são uma forma especial de pesquisa linguística e rotinas de comparação. Em um comparador com reconhecimento de cultura, o conceito de um elemento de agrupamento é estendido para incluir informações específicas para a cultura especificada.

Por exemplo, [no alfabeto húngaro](https://en.wikipedia.org/wiki/Hungarian_alphabet), quando os dois caracteres \<dz\> aparecem de volta para trás, eles são considerados sua própria letra exclusiva distinta de \<d\> ou \<z\> . Isso significa que \<dz\> , quando é visto em uma cadeia de caracteres, um comparador com reconhecimento de cultura húngaro trata isso como um único elemento de agrupamento.

| String | Como elementos de agrupamento | Comentários |
|---|---|---|
| `"endz"` | `"e" + "n" + "d" + "z"` | (usando um comparador linguístico padrão) |
| `"endz"` | `"e" + "n" + "dz"` | (usando um comparador com reconhecimento de cultura húngaro) |

Ao usar um comparador com reconhecimento de cultura húngaro, isso significa que a cadeia de caracteres `"endz"` *não* termina com a subcadeia de caracteres `"z"` , pois < \dz \> e < \Z \> são considerados elementos de agrupamento com significado semântico diferente.

```cs
// Set thread culture to Hungarian
CultureInfo.CurrentCulture = CultureInfo.GetCultureInfo("hu-HU");
Console.WriteLine("endz".EndsWith("z")); // Prints 'False'

// Set thread culture to invariant culture
CultureInfo.CurrentCulture = CultureInfo.InvariantCulture;
Console.WriteLine("endz".EndsWith("z")); // Prints 'True'
```

> [!NOTE]
>
> - Comportamento: os comparadores lingüísticas e com reconhecimento de cultura podem sofrer ajustes de comportamento de tempos em tempos. O ICU e o recurso NLS mais antigo do Windows são atualizados para considerar como as linguagens do mundo mudam. Para obter mais informações, consulte a variação de dados de localidade da postagem do blog [(cultura)](/archive/blogs/shawnste/locale-culture-data-churn). O comportamento do comparador *ordinal* nunca será alterado, já que ele executa a comparação e a pesquisa de bits exatas. No entanto, o comportamento do comparador de *OrdinalIgnoreCase* pode mudar conforme o Unicode cresce para abranger mais conjuntos de caracteres e corrigir omissões em dados de maiúsculas e minúsculas existentes.
> - Uso: os comparadores `StringComparison.InvariantCulture` e `StringComparison.InvariantCultureIgnoreCase` são comparadores lingüísticos que não reconhecem a cultura. Ou seja, esses comparadores entendem conceitos como o caractere acentuado é ter várias representações subjacentes possíveis e que todas essas representações devem ser tratadas iguais. Mas os comparadores lingüísticos que não reconhecem a cultura não conterão tratamento especial para \<dz\> o as \<d\> \<z\> , conforme mostrado acima. Eles também não são caracteres especiais como o alemão Eszett (ß).

O .NET também oferece o *modo de globalização invariável*. Esse modo de aceitação desabilita caminhos de código que lidam com rotinas de comparação e pesquisa linguística. Nesse modo, todas as operações usam comportamentos *ordinais* ou *OrdinalIgnoreCase* , independentemente do `CultureInfo` argumento ou que `StringComparison` o chamador fornece. Para obter mais informações, consulte [Opções de configuração de tempo de execução para globalização](../../core/run-time-config/globalization.md) e [modo invariável de globalização do .NET Core](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md).

Para obter mais informações, consulte [práticas recomendadas para comparar cadeias de caracteres no .net](best-practices-strings.md).

## <a name="security-implications"></a>Implicações de segurança

Se seu aplicativo usar uma API afetada para filtragem, é recomendável habilitar as regras de análise de código CA1307 e CA1309 para ajudar a localizar locais onde uma pesquisa linguística pode ter sido usada inadvertidamente em vez de uma pesquisa ordinal. Os padrões de código como os seguintes podem ser suscetíveis a explorações de segurança.

```cs
//
// THIS SAMPLE CODE IS INCORRECT.
// DO NOT USE IT IN PRODUCTION.
//
public bool ContainsHtmlSensitiveCharacters(string input)
{
    if (input.IndexOf("<") >= 0) { return true; }
    if (input.IndexOf("&") >= 0) { return true; }
    return false;
}
```

Como o `string.IndexOf(string)` método usa uma pesquisa linguística por padrão, é possível que uma cadeia de caracteres contenha um literal `'<'` ou `'&'` caractere e que a `string.IndexOf(string)` rotina seja retornada `-1` , indicando que a subcadeia de caracteres de pesquisa não foi encontrada. As regras de análise de código CA1307 e CA1309 sinalizam sites de chamada e alertam o desenvolvedor de que há um problema potencial.

## <a name="default-search-and-comparison-types"></a>Tipos de comparação e pesquisa padrão

A tabela a seguir lista os tipos de comparação e de pesquisa padrão para várias APIs de cadeia de caracteres e semelhantes a cadeia. Se o chamador fornecer um `CultureInfo` parâmetro ou explícito `StringComparison` , esse parâmetro será respeitado em qualquer padrão.

| API | Comportamento padrão | Comentários |
|---|---|---|
| `string.Compare` | CurrentCulture | |
| `string.CompareTo` | CurrentCulture | |
| `string.Contains` | Ordinal | |
| `string.EndsWith` | Ordinal | (quando o primeiro parâmetro é um `char` ) |
| `string.EndsWith` | CurrentCulture | (quando o primeiro parâmetro é um `string` ) |
| `string.Equals` | Ordinal | |
| `string.GetHashCode` | Ordinal | |
| `string.IndexOf` | Ordinal | (quando o primeiro parâmetro é um `char` ) |
| `string.IndexOf` | CurrentCulture | (quando o primeiro parâmetro é um `string` ) |
| `string.IndexOfAny` | Ordinal | |
| `string.LastIndexOf` | Ordinal | (quando o primeiro parâmetro é um `char` ) |
| `string.LastIndexOf` | CurrentCulture | (quando o primeiro parâmetro é um `string` ) |
| `string.LastIndexOfAny` | Ordinal | |
| `string.Replace` | Ordinal | |
| `string.Split` | Ordinal | |
| `string.StartsWith` | Ordinal | (quando o primeiro parâmetro é um `char` ) |
| `string.StartsWith` | CurrentCulture | (quando o primeiro parâmetro é um `string` ) |
| `string.ToLower` | CurrentCulture | |
| `string.ToLowerInvariant` | InvariantCulture | |
| `string.ToUpper` | CurrentCulture | |
| `string.ToUpperInvariant` | InvariantCulture | |
| `string.Trim` | Ordinal | |
| `string.TrimEnd` | Ordinal | |
| `string.TrimStart` | Ordinal | |
| `string == string` | Ordinal | |
| `string != string` | Ordinal | |

Ao contrário das `string` APIs, todas as `MemoryExtensions` APIs executam pesquisas e comparações *ordinais* por padrão, com as seguintes exceções.

| API | Comportamento padrão | Comentários |
|---|---|---|
| `MemoryExtensions.ToLower` | CurrentCulture | (quando passado um `CultureInfo` argumento nulo) |
| `MemoryExtensions.ToLowerInvariant` | InvariantCulture | |
| `MemoryExtensions.ToUpper` | CurrentCulture | (quando passado um `CultureInfo` argumento nulo) |
| `MemoryExtensions.ToUpperInvariant` | InvariantCulture | |

Uma consequência é que, ao converter o código do consumo `string` para o consumo `ReadOnlySpan<char>` , as alterações comportamentais podem ser introduzidas inadvertidamente. Veja a seguir um exemplo disso.

```cs
string str = GetString();
if (str.StartsWith("Hello")) { /* do something */ } // this is a CULTURE-AWARE (linguistic) comparison

ReadOnlySpan<char> span = s.AsSpan();
if (span.StartsWith("Hello")) { /* do something */ } // this is an ORDINAL (non-linguistic) comparison
```

A maneira recomendada para resolver isso é passar um parâmetro explícito `StringComparison` para essas APIs. As regras de análise de código CA1307 e CA1309 podem ajudar com isso.

```cs
string str = GetString();
if (str.StartsWith("Hello", StringComparison.Ordinal)) { /* do something */ } // ordinal comparison

ReadOnlySpan<char> span = s.AsSpan();
if (span.StartsWith("Hello", StringComparison.Ordinal)) { /* do something */ } // ordinal comparison
```

## <a name="see-also"></a>Confira também

- [Alterações interruptivas de globalização](../../core/compatibility/globalization.md)
- [Práticas recomendadas para comparar cadeias de caracteres no .NET](best-practices-strings.md)
- [Como comparar cadeias de caracteres no C#](../../csharp/how-to/compare-strings.md)
- [Globalização e ICU do .NET](../globalization-localization/globalization-icu.md)
- [Operações de cadeia de caracteres ordinal e sensível à cultura](/dotnet/api/system.string#ordinal-vs-culture-sensitive-operations)
- [Visão geral da análise de código-fonte do .NET](../../fundamentals/code-analysis/overview.md)
