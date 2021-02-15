---
ms.openlocfilehash: 719f336e1b38597674d6ee8f0c5429dd965054b1
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031957"
---
### <a name="floating-point-formatting-and-parsing-behavior-changed"></a>Comportamento de análise e formatação de ponto flutuante alterado

A análise de ponto flutuante e o comportamento de formatação (pelos <xref:System.Double> <xref:System.Single> tipos e) agora são compatíveis com IEEE.

#### <a name="change-description"></a>Descrição das alterações

No .NET Core 2,2 e versões anteriores, Formatar com <xref:System.Double.ToString%2A?displayProperty=nameWithType> e e <xref:System.Single.ToString%2A?displayProperty=nameWithType> analisar com <xref:System.Double.Parse%2A?displayProperty=nameWithType> ,, e <xref:System.Double.TryParse%2A?displayProperty=nameWithType> <xref:System.Single.Parse%2A?displayProperty=nameWithType> <xref:System.Single.TryParse%2A?displayProperty=nameWithType> não são compatíveis com IEEE. Como resultado, é impossível garantir que um valor seja arvoltado com qualquer cadeia de caracteres de formato padrão ou personalizada com suporte. Para algumas entradas, a tentativa de analisar um valor formatado pode falhar e, para outros, o valor analisado não é igual ao valor original.

A partir do .NET Core 3,0, as operações de análise e formatação são compatíveis com o IEEE 754. Isso garante que o comportamento dos tipos de ponto flutuante no .NET corresponda ao de linguagens compatíveis com IEEE, como C#. Para obter mais informações, consulte a postagem de [ponto flutuante e melhorias de formatação no blog do .NET Core 3,0](https://devblogs.microsoft.com/dotnet/floating-point-parsing-and-formatting-improvements-in-net-core-3-0/) .

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="recommended-action"></a>Ação recomendada

A seção "impacto potencial para código existente" das [melhorias de análise de ponto flutuante e de formatação na](https://devblogs.microsoft.com/dotnet/floating-point-parsing-and-formatting-improvements-in-net-core-3-0/) postagem de blog do .net Core 3,0 sugere alterações no código se você observar uma alteração de comportamento quando comparada aos aplicativos .net Core 2,2 em geral, isso envolve o uso de uma cadeia de caracteres de formato padrão ou personalizada diferente para impor o comportamento desejado. Alguns resultados podem não ter uma solução alternativa se eles estavam incorretos anteriormente.

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Double.ToString%2A?displayProperty=nameWithType>
- <xref:System.Single.ToString%2A?displayProperty=nameWithType>
- <xref:System.Double.Parse%2A?displayProperty=nameWithType>
- <xref:System.Double.TryParse%2A?displayProperty=nameWithType>
- <xref:System.Single.Parse%2A?displayProperty=nameWithType>
- <xref:System.Single.TryParse%2A?displayProperty=nameWithType>

<!-- 

#### Affected APIs

- `Overload:System.Double.ToString`
- `Overload:System.Single.ToString`
- `Overload:System.Double.Parse`
- `Overload:System.Double.TryParse`
- `Overload:System.Single.Parse`
- `Overload:System.Single.TryParse`

-->
