---
description: 'Saiba mais sobre: numéricos no .NET'
title: Numéricos no .NET
ms.date: 10/18/2018
helpviewer_keywords:
- SIMD
- System.Numerics.Vectors
- vectors
- scientific computing
- Complex
- numerics
- BigInteger
ms.assetid: dfebc18e-acde-4510-9fa7-9a0f4aa3bd11
ms.openlocfilehash: 386b5322a19b1f59358a941d7c37f7e5a81df30c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99731663"
---
# <a name="numerics-in-net"></a>Numéricos no .NET

O .NET fornece uma variedade de inteiros numéricos e primitivos de ponto flutuante, bem como <xref:System.Numerics.BigInteger?displayProperty=nameWithType>, que é um tipo integral sem limite teórico superior ou inferior, <xref:System.Numerics.Complex?displayProperty=nameWithType>, que representa números complexos e um conjunto de tipos habilitados para SIMD no namespace <xref:System.Numerics>.
  
## <a name="integer-types"></a>Tipos de inteiro

O .NET dá suporte a tipos inteiros tanto com sinal quanto sem sinal de 8, 16, 32 e 64 bits, que estão listados na tabela a seguir:
  
|Tipo|Assinado/não assinado|Tamanho (em bytes)|Valor mínimo|Valor máximo|  
|----------|----------------------|--------------------|-------------------|-------------------|  
|<xref:System.Byte?displayProperty=nameWithType>|Não assinado|1|0|255|  
|<xref:System.Int16?displayProperty=nameWithType>|Com sinal|2|-32,768|32.767|  
|<xref:System.Int32?displayProperty=nameWithType>|Com sinal|4|-2,147,483,648|2\.147.483.647|  
|<xref:System.Int64?displayProperty=nameWithType>|Com sinal|8|-9,223,372,036,854,775,808|9,223,372,036,854,775,807|  
|<xref:System.SByte?displayProperty=nameWithType>|Com sinal|1|-128|127|  
|<xref:System.UInt16?displayProperty=nameWithType>|Não assinado|2|0|65.535|  
|<xref:System.UInt32?displayProperty=nameWithType>|Não assinado|4|0|4,294,967,295|  
|<xref:System.UInt64?displayProperty=nameWithType>|Não assinado|8|0|18,446,744,073,709,551,615|  
  
Cada tipo inteiro dá suporte a um conjunto de operadores aritméticos padrão. A classe <xref:System.Math?displayProperty=nameWithType> fornece métodos para um conjunto mais amplo de funções matemáticas.

Você também pode trabalhar com os bits individuais nos valores usando a classe <xref:System.BitConverter?displayProperty=nameWithType>.  

> [!NOTE]  
> Os tipos de inteiro sem sinal não estão em conformidade com CLS. Para saber mais, veja [Componentes de independência de linguagem e componentes independentes da linguagem](language-independence-and-language-independent-components.md).

## <a name="biginteger"></a>BigInteger

A estrutura <xref:System.Numerics.BigInteger?displayProperty=nameWithType> é um tipo imutável que representa um inteiro arbitrariamente grande cujo valor, em teoria, não tem limites superiores ou inferiores. Os métodos do tipo <xref:System.Numerics.BigInteger> são muito semelhantes aos dos outros tipos integrais.
  
## <a name="floating-point-types"></a>Tipos de ponto flutuante

O .NET inclui três primitivos tipos de ponto flutuante, que estão listados na tabela a seguir:
  
|Tipo|Tamanho (em bytes)|Intervalo aproximado|Precisão|  
|----------|--------|---------------------|--------------------|  
|<xref:System.Single?displayProperty=nameWithType>|4|±1,5 x 10<sup>−45</sup> para ±3,4 x 10<sup>38</sup>|~6 a 9 dígitos|  
|<xref:System.Double?displayProperty=nameWithType>|8|±5.0 × 10<sup>−324</sup> to ±1.7 × 10<sup>308</sup>|~15 a 17 dígitos|  
|<xref:System.Decimal?displayProperty=nameWithType>|16|±1,0 x 10<sup>-28</sup> para ±7,9228 x 10<sup>28</sup>|28 a 29 dígitos|  
  
Os tipos <xref:System.Single> e <xref:System.Double> dão suporte a valores especiais que representam não é um número e infinito. Por exemplo, o tipo <xref:System.Double> fornece os seguintes valores: <xref:System.Double.NaN?displayProperty=nameWithType>, <xref:System.Double.NegativeInfinity?displayProperty=nameWithType> e <xref:System.Double.PositiveInfinity?displayProperty=nameWithType>. Você usa os métodos <xref:System.Double.IsNaN%2A?displayProperty=nameWithType>, <xref:System.Double.IsInfinity%2A?displayProperty=nameWithType>, <xref:System.Double.IsPositiveInfinity%2A?displayProperty=nameWithType> e <xref:System.Double.IsNegativeInfinity%2A?displayProperty=nameWithType> para testar esses valores especiais.

Cada tipo de ponto flutuante dá suporte a um conjunto de operadores aritméticos padrão. A classe <xref:System.Math?displayProperty=nameWithType> fornece métodos para um conjunto mais amplo de funções matemáticas. O .NET Core 2,0 e posterior inclui a <xref:System.MathF?displayProperty=nameWithType> classe, que fornece métodos que aceitam argumentos do <xref:System.Single> tipo.

Você também pode trabalhar com os bits individuais nos valores <xref:System.Double> e <xref:System.Single> usando a classe <xref:System.BitConverter?displayProperty=nameWithType>. A estrutura <xref:System.Decimal?displayProperty=nameWithType> tem seus próprios métodos <xref:System.Decimal.GetBits%2A?displayProperty=nameWithType> e <xref:System.Decimal.%23ctor%28System.Int32%5B%5D%29>, para trabalhar com os bits individuais de um valor decimal, assim como seu próprio conjunto de métodos para executar algumas operações matemáticas adicionais.
  
Os <xref:System.Double> <xref:System.Single> tipos e devem ser usados para valores que, por sua natureza, são imprecisos (por exemplo, a distância entre duas estrelas) e para aplicativos nos quais um alto grau de precisão e erro de arredondamento pequeno não é necessário. Use o <xref:System.Decimal?displayProperty=nameWithType> tipo para casos em que maior precisão é necessária e os erros de arredondamento devem ser minimizados.

> [!NOTE]
> O tipo <xref:System.Decimal> não elimina a necessidade de arredondamento. Em vez disso, ele minimiza erros devido a arredondamento.
  
## <a name="complex"></a>Complex

A estrutura <xref:System.Numerics.Complex?displayProperty=nameWithType> representa um número complexo, ou seja, um número com uma parte de número real e uma parte de número imaginário. Dá suporte a um conjunto padrão de aritmética, de comparação, de igualdade, de conversões explícita e implícita, bem como a métodos matemáticos, algébricos e trigonométricos.  
  
## <a name="simd-enabled-types"></a>Tipos habilitados para SIMD

O namespace <xref:System.Numerics> inclui um conjunto de tipos habilitados para SIMD do .NET. Operações SIMD (Single Instruction Multiple Data) podem ser paralelizadas no nível de hardware. Isso aumenta a taxa de transferência dos cálculos vetorizadas, que são comuns em aplicativos matemáticos, científicos e gráficos.
  
Os tipos habilitados para SIMD do .NET incluem o seguinte:

- Os tipos <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3> e <xref:System.Numerics.Vector4>, que representam vetores com 2, 3 e 4 valores de <xref:System.Single>.

- Dois tipos de matriz, <xref:System.Numerics.Matrix3x2>, que representa uma matriz 3x2, e <xref:System.Numerics.Matrix4x4>, que representa uma matriz 4x4.

- O tipo <xref:System.Numerics.Plane> representa um plano no espaço tridimensional.

- O tipo <xref:System.Numerics.Quaternion>, que representa um vetor usado para codificar rotações físicas tridimensionais.

- O tipo <xref:System.Numerics.Vector%601>, que representa um vetor de um tipo numérico especificado e fornece um amplo conjunto de operadores que se beneficiam de suporte a SIMD. A contagem de uma instância <xref:System.Numerics.Vector%601> é corrigida, mas seu valor <xref:System.Numerics.Vector%601.Count%2A?displayProperty=nameWithType> depende da CPU do computador em que o código é executado.

  > [!NOTE]
  > O <xref:System.Numerics.Vector%601> tipo é incluído no .NET Core e no .NET 5 +, mas não .NET Framework. Se você estiver usando .NET Framework, instale o pacote NuGet [System. Numerics. vetores](https://www.nuget.org/packages/System.Numerics.Vectors) para obter acesso a esse tipo.
  
Os tipos habilitados para SIMD são implementados de modo que possam ser usados com hardware não habilitados para SIMD ou compiladores JIT. Para aproveitar as instruções de SIMD, seus aplicativos de 64 bits devem ser executados pelo tempo de execução que usa o compilador RyuJIT, que está incluído no .NET Core e no .NET Framework 4,6 e versões posteriores. Ele adiciona suporte a SIMD quando tem processadores de 64 bits como destino.

Para obter mais informações, consulte [usar tipos numéricos acelerados por SIMD](simd.md).

## <a name="see-also"></a>Consulte também

- [Cadeias de Caracteres de Formato Numérico Padrão](base-types/standard-numeric-format-strings.md)
