---
title: 'Alteração significativa: categoria Unicode alterada para alguns caracteres latinos-1'
description: Saiba mais sobre a alteração significativa de globalização no .NET 5,0, em que os métodos Char agora retornam a categoria Unicode correta para caracteres no intervalo Latin-1.
ms.date: 04/07/2020
ms.openlocfilehash: 8bd093a89857c83921fc0bf987348b529f74ce68
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760538"
---
# <a name="unicode-category-changed-for-some-latin-1-characters"></a>Categoria Unicode alterada para alguns caracteres latinos-1

<xref:System.Char> Agora, os métodos retornam a categoria Unicode correta para os caracteres no intervalo Latin-1. A categoria corresponde à do padrão Unicode.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, os <xref:System.Char> métodos usaram uma lista fixa de categorias Unicode para caracteres no intervalo Latin-1. No entanto, o padrão Unicode alterou as categorias de alguns desses caracteres desde que essas APIs foram implementadas, criando uma discrepância. Além disso, também havia uma discrepância entre <xref:System.Char> <xref:System.Globalization.CharUnicodeInfo> as APIs e, que seguem o padrão Unicode. No .NET 5,0 e versões posteriores, <xref:System.Char> os métodos usam e retornam a categoria Unicode que corresponde ao padrão Unicode para todos os caracteres.

A tabela a seguir mostra os caracteres cujas categorias Unicode foram alteradas no .NET 5,0:

| Caractere    | Categoria Unicode<br>nas versões anteriores do .NET | Categoria Unicode<br>no .NET 5,0 e versões posteriores |
|:------------:|:---------------------------------------------:|:--------------------------------------------------:|
| § (\u00a7)   | `OtherSymbol`                                 | `OtherPunctuation`                                 |
| ª (\u00aa)   | `LowercaseLetter`                             | `OtherLetter`                                      |
| \U00ad (baixo) | `DashPunctuation`                             | `Format`                                           |
| ¶ (\u00b6)   | `OtherSymbol`                                 | `OtherPunctuation`                                 |
| º (\u00ba)   | `LowercaseLetter`                             | `OtherLetter`                                      |

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

Se você tiver qualquer código que obtém a categoria de caracteres Unicode usando a <xref:System.Char> classe e supõe que a categoria nunca será alterada, talvez seja necessário atualizá-la.

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi feita para que as categorias retornadas pelo <xref:System.Char> tipo sejam consistentes com o padrão Unicode e o <xref:System.Globalization.CharUnicodeInfo> tipo.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Char.GetUnicodeCategory%2A?displayProperty=fullName>
- <xref:System.Char.IsLetter%2A?displayProperty=fullName>
- <xref:System.Char.IsPunctuation%2A?displayProperty=fullName>
- <xref:System.Char.IsSymbol%2A?displayProperty=fullName>
- <xref:System.Char.IsLower%2A?displayProperty=fullName>

Além disso, qualquer classe que depende de <xref:System.Char> obter a categoria de caractere Unicode, por exemplo, <xref:System.Text.RegularExpressions.Regex> , é afetada por essa alteração.

<!--

### Affected APIs

- `Overload:System.Char.GetUnicodeCategory`
- `Overload:System.Char.IsLetter`
- `Overload:System.Char.IsPunctuation`
- `Overload:System.Char.IsSymbol`
- `Overload:System.Char.IsLower`

### Category

- Core .NET libraries
- Globalization
-
-->
