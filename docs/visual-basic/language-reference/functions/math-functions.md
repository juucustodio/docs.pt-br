---
description: 'Saiba mais sobre: funções matemáticas (Visual Basic)'
title: Funções matemáticas
ms.date: 01/27/2020
helpviewer_keywords:
- math functions, Visual Basic
- arithmetic operations, math functions
- math routines
- Atn function
ms.assetid: 4d2d82e7-6924-42fe-a4a7-b4dd5bebbd0c
ms.openlocfilehash: d6ab82e45a17c0b1e1ee9f7df54936cd5420ef2b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99731096"
---
# <a name="math-functions-visual-basic"></a>Funções matemáticas (Visual Basic)

Os métodos da <xref:System.Math?displayProperty=nameWithType> classe fornecem funções matemáticas, logarítmicas e outros tipos matemáticos comuns.

## <a name="remarks"></a>Comentários

A tabela a seguir lista os métodos da <xref:System.Math?displayProperty=nameWithType> classe. Você pode usá-los em um programa Visual Basic:
  
|Método .NET|Descrição|
|---------------------------|-----------------|
|<xref:System.Math.Abs%2A>|Retorna o valor absoluto de um número.|
|<xref:System.Math.Acos%2A>|Retorna o ângulo cujo cosseno é o número especificado.|
|<xref:System.Math.Asin%2A>|Retorna o ângulo cujo seno é o número especificado.|
|<xref:System.Math.Atan%2A>|Retorna o ângulo cuja tangente é o número especificado.|
|<xref:System.Math.Atan2%2A>|Retorna o ângulo cuja tangente é o quociente de dois números especificados.|
|<xref:System.Math.BigMul%2A>|Retorna o produto completo de números de 2 32 bits.|
|<xref:System.Math.Ceiling%2A>|Retorna o menor valor integral maior ou igual ao especificado `Decimal` ou `Double` .|
|<xref:System.Math.Cos%2A>|Retorna o cosseno do ângulo especificado.|
|<xref:System.Math.Cosh%2A>|Retorna o cosseno hiperbólico do ângulo especificado.|
|<xref:System.Math.DivRem%2A>|Retorna o quociente de números inteiros com sinal de 2 32 bits ou 64 e também retorna o resto em um parâmetro de saída.|
|<xref:System.Math.Exp%2A>|Retorna e (a base de logaritmos naturais) é gerada para a potência especificada.|
|<xref:System.Math.Floor%2A>|Retorna o maior inteiro que é menor ou igual ao especificado ou ao `Decimal` `Double` número.|
|<xref:System.Math.IEEERemainder%2A>|Retorna o resto que resulta da divisão de um número especificado por outro número especificado.|
|<xref:System.Math.Log%2A>|Retorna o logaritmo natural (base e) de um número especificado ou o logaritmo de um número especificado em uma base especificada.|
|<xref:System.Math.Log10%2A>|Retorna o logaritmo de base 10 de um número especificado.|
|<xref:System.Math.Max%2A>|Retorna o maior de dois números.|
|<xref:System.Math.Min%2A>|Retorna o menor de dois números.|
|<xref:System.Math.Pow%2A>|Retorna um número especificado elevado à potência especificada.|
|<xref:System.Math.Round%2A>|Retorna um `Decimal` `Double` valor ou arredondado para o valor integral mais próximo ou para um número especificado de dígitos fracionários.|
|<xref:System.Math.Sign%2A>|Retorna um `Integer` valor que indica o sinal de um número.|
|<xref:System.Math.Sin%2A>|Retorna o seno do ângulo especificado.|
|<xref:System.Math.Sinh%2A>|Retorna o seno hiperbólico do ângulo especificado.|
|<xref:System.Math.Sqrt%2A>|Retorna a raiz quadrada de um número especificado.|
|<xref:System.Math.Tan%2A>|Retorna a tangente do ângulo especificado.|
|<xref:System.Math.Tanh%2A>|Retorna a tangente hiperbólica do ângulo especificado.|
|<xref:System.Math.Truncate%2A>|Calcula a parte integral de um `Decimal` número ou especificado `Double` .|

A tabela a seguir lista os métodos da <xref:System.Math?displayProperty=nameWithType> classe que não existem no .NET Framework, mas que são adicionados no .net Standard ou no .NET Core:

|Método .NET|Descrição|Disponível em|
|---------------------------|-----------------|-----------|
|<xref:System.Math.Acosh%2A>|Retorna o ângulo cujo cosseno hiperbólico é o número especificado.|A partir do .NET Core 2,1 e .NET Standard 2,1|
|<xref:System.Math.Asinh%2A>|Retorna o ângulo cujo seno hiperbólico é o número especificado.|A partir do .NET Core 2,1 e .NET Standard 2,1|
|<xref:System.Math.Atanh%2A>|Retorna o ângulo cuja tangente hiperbólica é o número especificado.|A partir do .NET Core 2,1 e .NET Standard 2,1|
|<xref:System.Math.BitDecrement%2A>|Retorna o próximo valor menor que é comparado como menor que `x`.|A partir do .NET Core 3,0|
|<xref:System.Math.BitIncrement%2A>|Retorna o próximo valor maior que é comparado como maior que `x`.|A partir do .NET Core 3,0|
|<xref:System.Math.Cbrt%2A>|Retorna a raiz cúbica de um número especificado.|A partir do .NET Core 2,1 e .NET Standard 2,1|
|<xref:System.Math.Clamp%2A>|Retorna `value` fixado no intervalo inclusivo de `min` e `max`.|A partir do .NET Core 2,0 e .NET Standard 2,1|
|<xref:System.Math.CopySign%2A>|Retorna um valor com magnitude de `x` e o sinal de `y`.|A partir do .NET Core 3,0|
|<xref:System.Math.FusedMultiplyAdd%2A>|Retorna (x \* y) + z, arredondado como uma operação ternário.|A partir do .NET Core 3,0|
|<xref:System.Math.ILogB%2A>|Retorna o logaritmo inteiro de base 2 de um número especificado.|A partir do .NET Core 3,0|
|<xref:System.Math.Log2%2A>|Retorna o logaritmo de base 2 de um número especificado.|A partir do .NET Core 3,0|
|<xref:System.Math.MaxMagnitude%2A>|Retorna a maior magnitude de dois números de ponto flutuante de precisão dupla.|A partir do .NET Core 3,0|
|<xref:System.Math.MinMagnitude%2A>|Retorna a menor magnitude de dois números de ponto flutuante de precisão dupla.|A partir do .NET Core 3,0|
|<xref:System.Math.ScaleB%2A>|Retorna x \* 2 ^ n computado com eficiência.|A partir do .NET Core 3,0|

Para usar essas funções sem qualificação, importe o <xref:System.Math?displayProperty=nameWithType> namespace em seu projeto adicionando o seguinte código à parte superior do seu arquivo de origem:

```vb
Imports System.Math
```

## <a name="example---abs"></a>Exemplo – ABS

Este exemplo usa o <xref:System.Math.Abs%2A> método da <xref:System.Math> classe para computar o valor absoluto de um número.

```vb
Dim x As Double = Math.Abs(50.3)
Dim y As Double = Math.Abs(-50.3)
Console.WriteLine(x)
Console.WriteLine(y)
' This example produces the following output:
' 50.3
' 50.3
```  

## <a name="example---atan"></a>Exemplo – ATAN

Este exemplo usa o <xref:System.Math.Atan%2A> método da <xref:System.Math> classe para calcular o valor de PI.

```vb
Public Function GetPi() As Double
    ' Calculate the value of pi.
    Return 4.0 * Math.Atan(1.0)
End Function
```

> [!NOTE]
> A <xref:System.Math?displayProperty=nameWithType> classe contém o <xref:System.Math.PI?displayProperty=nameWithType> campo constante. Você pode usá-lo em vez de calcular.

## <a name="example---cos"></a>Exemplo-cos

Este exemplo usa o <xref:System.Math.Cos%2A> método da <xref:System.Math> classe para retornar o cosseno de um ângulo.

```vb
Public Function Sec(angle As Double) As Double
    ' Calculate the secant of angle, in radians.
    Return 1.0 / Math.Cos(angle)
End Function
```

## <a name="example---exp"></a>Exemplo – exp

Este exemplo usa o <xref:System.Math.Exp%2A> método da <xref:System.Math> classe para retornar e elevado a uma potência.

```vb
Public Function Sinh(angle As Double) As Double
    ' Calculate hyperbolic sine of an angle, in radians.
    Return (Math.Exp(angle) - Math.Exp(-angle)) / 2.0
End Function
```

## <a name="example---log"></a>Exemplo-log

Este exemplo usa o <xref:System.Math.Log%2A> método da <xref:System.Math> classe para retornar o logaritmo natural de um número.

```vb
Public Function Asinh(value As Double) As Double
    ' Calculate inverse hyperbolic sine, in radians.
    Return Math.Log(value + Math.Sqrt(value * value + 1.0))
End Function
```

## <a name="example---round"></a>Exemplo – redondo

Este exemplo usa o <xref:System.Math.Round%2A> método da <xref:System.Math> classe para arredondar um número para o número inteiro mais próximo.

```vb
Dim myVar2 As Double = Math.Round(2.8)
Console.WriteLine(myVar2)
' The code produces the following output:
' 3
```

## <a name="example---sign"></a>Exemplo-assinar

Este exemplo usa o <xref:System.Math.Sign%2A> método da <xref:System.Math> classe para determinar o sinal de um número.

```vb
Dim mySign1 As Integer = Math.Sign(12)
Dim mySign2 As Integer = Math.Sign(-2.4)
Dim mySign3 As Integer = Math.Sign(0)
Console.WriteLine(mySign1)
Console.WriteLine(mySign2)
Console.WriteLine(mySign3)
' The code produces the following output:
' 1
' -1
' 0
```

## <a name="example---sin"></a>Exemplo-Sin

Este exemplo usa o <xref:System.Math.Sin%2A> método da <xref:System.Math> classe para retornar o seno de um ângulo.

```vb
Public Function Csc(angle As Double) As Double
    ' Calculate cosecant of an angle, in radians.
    Return 1.0 / Math.Sin(angle)
End Function
```

## <a name="example---sqrt"></a>Exemplo – sqrt

Este exemplo usa o <xref:System.Math.Sqrt%2A> método da <xref:System.Math> classe para calcular a raiz quadrada de um número.

```vb
Dim mySqrt1 As Double = Math.Sqrt(4)
Dim mySqrt2 As Double = Math.Sqrt(23)
Dim mySqrt3 As Double = Math.Sqrt(0)
Dim mySqrt4 As Double = Math.Sqrt(-4)
Console.WriteLine(mySqrt1)
Console.WriteLine(mySqrt2)
Console.WriteLine(mySqrt3)
Console.WriteLine(mySqrt4)
' The code produces the following output:
' 2
' 4.79583152331272
' 0
' NaN
```

## <a name="example---tan"></a>Exemplo-Tan

Este exemplo usa o <xref:System.Math.Tan%2A> método da <xref:System.Math> classe para retornar a tangente de um ângulo.

```vb
Public Function Ctan(angle As Double) As Double
    ' Calculate cotangent of an angle, in radians.
    Return 1.0 / Math.Tan(angle)
End Function
```

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.VBMath.Rnd%2A>
- <xref:Microsoft.VisualBasic.VBMath.Randomize%2A>
- <xref:System.Double.NaN>
- [Funções Matemáticas Derivadas](../keywords/derived-math-functions.md)
- [Operadores aritméticos](../operators/arithmetic-operators.md)
