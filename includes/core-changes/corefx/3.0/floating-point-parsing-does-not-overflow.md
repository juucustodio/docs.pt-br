---
ms.openlocfilehash: 935d9b2368ea4a0eeca7943dcbd584d24d2a6633
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031958"
---
### <a name="floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception"></a>Operações de análise de ponto flutuante não falham mais ou geram uma estourexception

Os métodos de análise de ponto flutuante não geram mais um <xref:System.OverflowException> retorno ou retornam `false` quando analisam uma cadeia de caracteres cujo valor numérico está fora do intervalo do <xref:System.Single> tipo de <xref:System.Double> ponto flutuante.

#### <a name="change-description"></a>Descrição das alterações

No .NET Core 2,2 e versões anteriores, os <xref:System.Double.Parse%2A?displayProperty=nameWithType> <xref:System.Single.Parse%2A?displayProperty=nameWithType> métodos e geram um <xref:System.OverflowException> para valores que estão fora do intervalo de seus respectivos tipos. Os <xref:System.Double.TryParse%2A?displayProperty=nameWithType> <xref:System.Single.TryParse%2A?displayProperty=nameWithType> métodos e retornam `false` para as representações de cadeia de caracteres de valores numéricos fora do intervalo.

A partir do .NET Core 3,0, <xref:System.Double.Parse%2A?displayProperty=nameWithType> os <xref:System.Double.TryParse%2A?displayProperty=nameWithType> métodos,, <xref:System.Single.Parse%2A?displayProperty=nameWithType> e <xref:System.Single.TryParse%2A?displayProperty=nameWithType> não falham mais ao analisar cadeias de caracteres numéricas fora do intervalo. Em vez disso, os <xref:System.Double> métodos de análise retornam <xref:System.Double.PositiveInfinity?displayProperty=nameWithType> valores que excedem <xref:System.Double.MaxValue?displayProperty=nameWithType> e retornam <xref:System.Double.NegativeInfinity?displayProperty=nameWithType> para valores menores que <xref:System.Double.MinValue?displayProperty=nameWithType> . Da mesma forma, os <xref:System.Single> métodos de análise retornam <xref:System.Single.PositiveInfinity?displayProperty=nameWithType> valores que excedem <xref:System.Single.MaxValue?displayProperty=nameWithType> e retornam <xref:System.Single.NegativeInfinity?displayProperty=nameWithType> valores menores que <xref:System.Single.MinValue?displayProperty=nameWithType> .

Essa alteração foi feita para melhorar a conformidade com o IEEE 754:2008.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="recommended-action"></a>Ação recomendada

Essa alteração pode afetar o código de uma das duas maneiras:

- Seu código depende do manipulador para o <xref:System.OverflowException> a ser executado quando ocorrer um estouro. Nesse caso, você deve remover a `catch` instrução e inserir qualquer código necessário em uma `If` instrução que testa se <xref:System.Double.IsInfinity%2A?displayProperty=nameWithType> ou <xref:System.Single.IsInfinity%2A?displayProperty=nameWithType> é `true` .

- Seu código supõe que os valores de ponto flutuante não são `Infinity` . Nesse caso, você deve adicionar o código necessário para verificar se há valores de ponto flutuante de `PositiveInfinity` e `NegativeInfinity` .

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Double.Parse%2A?displayProperty=nameWithType>
- <xref:System.Double.TryParse%2A?displayProperty=nameWithType>
- <xref:System.Single.Parse%2A?displayProperty=nameWithType>
- <xref:System.Single.TryParse%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:System.Double.Parse`
- `Overload:System.Double.TryParse`
- `Overload:System.Single.Parse`
- `Overload:System.Single.TryParse`

-->
