---
title: Tutorial Números em C# – introdução ao C#
description: Aprenda C# explorando tipos numéricos, seus usos, propriedades e métodos.
ms.date: 02/02/2021
ms.custom: mvc
ms.openlocfilehash: 253ecbc089722961013d058aff900bdde23fd366
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585631"
---
# <a name="manipulate-integral-and-floating-point-numbers-in-c"></a>Manipular números de ponto flutuante e integrais em C\#

Este tutorial ensina sobre os tipos numéricos em C# de maneira interativa. Você escreverá pequenas quantidades de código, depois compilará e executará esse código. O tutorial contém uma série de lições que exploram números e operações matemáticas em C#. Estas lições ensinam os princípios básicos da linguagem C#.

## <a name="prerequisites"></a>Pré-requisitos

O tutorial espera que você tenha uma máquina configurada para desenvolvimento local. No Windows, Linux ou macOS, você pode usar a CLI do .NET para criar, compilar e executar aplicativos. No Windows, você pode usar o Visual Studio 2019. Para obter instruções de instalação, consulte [configurar seu ambiente local](local-environment.md).

## <a name="explore-integer-math"></a>Explorar a matemática de inteiros

Crie um diretório chamado *numbers-quickstart*. Faça com que o diretório atual e execute o seguinte comando:

```dotnetcli
dotnet new console -n NumbersInCSharp -o .
```

Abra *Program.cs* em seu editor favorito e substitua a linha `Console.WriteLine("Hello World!");` pelo seguinte código:

```csharp
int a = 18;
int b = 6;
int c = a + b;
Console.WriteLine(c);
```

Execute este código digitando `dotnet run` na janela de comando.

Você viu uma das operações matemáticas fundamentais com números inteiros. O `int` tipo representa um número **inteiro**, zero, positivo ou inteiro negativo. Você usa o símbolo `+` para adição. Outras operações matemáticas comuns para inteiros incluem:

- `-` para subtração
- `*` para multiplicação
- `/` para divisão

Comece explorando essas diferentes operações. Adicione estas linhas após a linha que grava o valor de `c`:

```csharp

// subtraction
c = a - b;
Console.WriteLine(c);

// multiplication
c = a * b;
Console.WriteLine(c);

// division
c = a / b;
Console.WriteLine(c);
```

Execute este código digitando `dotnet run` na janela de comando.

Você também pode experimentar escrevendo várias operações matemáticas na mesma linha, se desejar. Experimente `c = a + b - 12 * 17;`, por exemplo. É permitido misturar variáveis e números constantes.

> [!TIP]
> À medida que explora C# (ou qualquer linguagem de programação), você cometerá erros ao escrever o código. O **compilador** encontrará esses erros e os reportará a você. Quando a saída contiver mensagens de erro, analise atentamente o código de exemplo e o código em sua janela para ver o que deve ser corrigido.
> Esse exercício ajudará você a conhecer a estrutura do código C#.

Você terminou a primeira etapa. Antes de iniciar a próxima seção, vamos passar o código atual para um método separado. Isso facilita o começo do trabalho com um exemplo novo. Renomeie seu método `Main` como `WorkingWithIntegers` e escreva um novo método `Main` que chama `WorkingWithIntegers`. Quando você terminar, seu código deverá ter a seguinte aparência:

```csharp
using System;

namespace NumbersInCSharp
{
    class Program
    {
        static void WorkingWithIntegers()
        {
            int a = 18;
            int b = 6;

            // addition
            int c = a + b;
            Console.WriteLine(c);

            // subtraction
            c = a - b;
            Console.WriteLine(c);

            // multiplication
            c = a * b;
            Console.WriteLine(c);

            // division
            c = a / b;
            Console.WriteLine(c);
        }

        static void Main(string[] args)
        {
            WorkingWithIntegers();
        }
    }
}
```

## <a name="explore-order-of-operations"></a>Explorar a ordem das operações

Comente a chamada para `WorkingWithIntegers()`. Isso tornará a saída menos congestionada enquanto você trabalha nesta seção:

```csharp
//WorkingWithIntegers();
```

O `//` inicia um **comentário** em C#. Os comentários são qualquer texto que você queira manter em seu código-fonte, mas não queria executar como código. O compilador não gera nenhum código executável de comentários.

A linguagem C# define a precedência de operações matemáticas diferentes com regras consistentes às regras que você aprendeu em matemática.
Multiplicação e divisão têm precedência sobre adição e subtração.
Explore isso adicionando o seguinte código ao seu método `Main` e executando `dotnet run`:

```csharp
int a = 5;
int b = 4;
int c = 2;
int d = a + b * c;
Console.WriteLine(d);
 ```

A saída demonstra que a multiplicação é executada antes da adição.

Você pode forçar uma ordem diferente de operações, adicionando parênteses para delimitar a operação, ou operações, que você quer realizar primeiro. Adicione as seguintes linhas e execute novamente:

```csharp
d = (a + b) * c;
Console.WriteLine(d);
```

Explore mais, combinando várias operações diferentes. Adicione algo parecido com as seguintes linhas na parte inferior de seu método `Main`. Tente `dotnet run` novamente.

```csharp
d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
Console.WriteLine(d);
```

Talvez você tenha observado um comportamento interessante com relação aos números inteiros. A divisão de inteiros sempre produz um resultado inteiro, mesmo quando você espera que o resultado inclua uma parte decimal ou fracionária.

Se você ainda não viu esse comportamento, tente o seguinte código ao final de seu método `Main`:

```csharp
int e = 7;
int f = 4;
int g = 3;
int h = (e + f) / g;
Console.WriteLine(h);
```

Digite `dotnet run` novamente para ver os resultados.

Antes de avançarmos, pegue todo código que você escreveu nesta seção e coloque-o em um novo método. Chame esse novo método de `OrderPrecedence`.
Você deve escrever algo assim:

```csharp
using System;

namespace NumbersInCSharp
{
    class Program
    {
        static void WorkingWithIntegers()
        {
            int a = 18;
            int b = 6;

            // addition
            int c = a + b;
            Console.WriteLine(c);

            // subtraction
            c = a - b;
            Console.WriteLine(c);

            // multiplication
            c = a * b;
            Console.WriteLine(c);

            // division
            c = a / b;
            Console.WriteLine(c);
        }

        static void OrderPrecedence()
        {
            int a = 5;
            int b = 4;
            int c = 2;
            int d = a + b * c;
            Console.WriteLine(d);

            d = (a + b) * c;
            Console.WriteLine(d);

            d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
            Console.WriteLine(d);

            int e = 7;
            int f = 4;
            int g = 3;
            int h = (e  + f) / g;
            Console.WriteLine(h);
        }

        static void Main(string[] args)
        {
            WorkingWithIntegers();

            OrderPrecedence();

        }
    }
}
```

## <a name="explore-integer-precision-and-limits"></a>Explorar a precisão de inteiros e limites

Esse último exemplo mostrou que uma divisão de inteiros trunca o resultado.
Você pode obter o **resto** usando o operador de **módulo** , o `%` caractere. Experimente o seguinte código em seu método `Main`:

```csharp
int a = 7;
int b = 4;
int c = 3;
int d = (a + b) / c;
int e = (a + b) % c;
Console.WriteLine($"quotient: {d}");
Console.WriteLine($"remainder: {e}");
```

O tipo de inteiro C# difere do inteiros matemáticos de outra forma: o tipo `int` tem limites mínimo e máximo. Adicione este código ao seu método `Main` para ver esses limites:

```csharp
int max = int.MaxValue;
int min = int.MinValue;
Console.WriteLine($"The range of integers is {min} to {max}");
```

Se um cálculo produzir um valor que excede esses limites, você terá uma condição de **estouro negativo** ou **estouro**. A resposta parece quebrar de um limite para o outro. Adicione estas duas linhas ao seu método `Main` para ver um exemplo:

```csharp
int what = max + 3;
Console.WriteLine($"An example of overflow: {what}");
```

Observe que a resposta é muito próxima do mínimo inteiro (negativo). É o mesmo que `min + 2`.
A operação de adição **estourou** os valores permitidos para números inteiros.
A resposta é um número negativo muito grande, pois um estouro "envolve" do maior valor de inteiro possível para o menor.

Há outros tipos numéricos com limites e precisão diferentes que você usaria quando o tipo `int` não atendesse às suas necessidades. Vamos explorar os outros tipos a seguir.

Novamente, vamos passar o código que você escreveu nesta seção para um método separado. Nomeie-o como `TestLimits`.

## <a name="work-with-the-double-type"></a>Trabalhar com o tipo Double

O tipo numérico `double` representa um número de ponto flutuante de precisão dupla. Esses termos podem ser novidade para você. Um número de **ponto flutuante** é útil para representar números não integrais que podem ser muito grandes ou pequenos em magnitude. A **precisão dupla** é um termo relativo que descreve o número de dígitos binários usados para armazenar o valor. Números de **precisão dupla** têm duas vezes o número de dígitos binários como **uma única precisão**. Em computadores modernos, é mais comum usar precisão dupla do que números de precisão única. Números de **precisão única** são declarados usando a `float` palavra-chave.
Vamos explorar. Adicione o seguinte código e veja o resultado:

```csharp
double a = 5;
double b = 4;
double c = 2;
double d = (a + b) / c;
Console.WriteLine(d);
```

Observe que a resposta inclui a parte decimal do quociente. Experimente uma expressão ligeiramente mais complicada com duplos:

```csharp
double e = 19;
double f = 23;
double g = 8;
double h = (e + f) / g;
Console.WriteLine(h);
```

O intervalo de um valor duplo é muito maior do que valores inteiros. Experimente o código a seguir abaixo do código que você escreveu até o momento:

```csharp
double max = double.MaxValue;
double min = double.MinValue;
Console.WriteLine($"The range of double is {min} to {max}");
```

Esses valores são impressos em notação científica. O número à esquerda do `E` é o significando. O número à direita é o expoente, como uma potência de 10.

Assim como os números decimais em matemática, os duplos em C# podem ter erros de arredondamento. Experimente esse código:

```csharp
double third = 1.0 / 3.0;
Console.WriteLine(third);
```

Você sabe que `0.3` repetir não é exatamente o mesmo que `1/3` .

***Desafio***

Tente outros cálculos com números grandes, números pequenos, multiplicação e divisão usando o `double` tipo. Experimente cálculos mais complicados.

Após algum tempo no desafio, pegue o código que você escreveu e coloque-o em um novo método. Chame esse novo método de `WorkWithDoubles`.

## <a name="work-with-decimal-types"></a>Trabalhar com tipos decimais

Você viu os tipos numéricos básicos em C#: inteiros e duplos.  Há um outro tipo para aprender: o `decimal` tipo. O tipo `decimal` tem um intervalo menor, mas precisão maior do que `double`. Vamos dar uma olhada:

```csharp
decimal min = decimal.MinValue;
decimal max = decimal.MaxValue;
Console.WriteLine($"The range of the decimal type is {min} to {max}");
```

Observe que o intervalo é menor do que o tipo `double`. Veja a precisão maior com o tipo decimal experimentando o código a seguir:

```csharp
double a = 1.0;
double b = 3.0;
Console.WriteLine(a / b);

decimal c = 1.0M;
decimal d = 3.0M;
Console.WriteLine(c / d);
```

O sufixo `M` nos números é o modo como você indica que uma constante deve usar o tipo `decimal`. Caso contrário, o compilador assume o `double` tipo.

> [!NOTE]
> A letra `M` foi escolhida como a letra mais visualmente distinta entre `double` as `decimal` palavras-chave e.

Observe que o cálculo usando o tipo decimal tem mais dígitos à direita da vírgula decimal.

***Desafio***

Agora que você viu os diferentes tipos numéricos, escreva um código que calcula a área de um círculo cujo raio é de 2,50 centímetros. Lembre-se de que a área de um círculo é o quadrado do raio multiplicado por PI. Uma dica: o .NET contém uma constante para PI, <xref:System.Math.PI?displayProperty=nameWithType>, que você pode usar para esse valor. <xref:System.Math.PI?displayProperty=nameWithType>, como todas as constantes declaradas no `System.Math` namespace, é um `double` valor. Por esse motivo, você deve usar `double` valores instead of `decimal` para esse desafio.

Você deve obter uma resposta entre 19 e 20.
Você pode verificar sua resposta [examinando o código de exemplo concluído no GitHub](https://github.com/dotnet/samples/tree/master/csharp/numbers-quickstart/Program.cs#L104-L106).

Experimente outras fórmulas, se quiser.

Você concluiu o início rápido "Números em C#". Continue com o início rápido [Branches e loops](branches-and-loops-local.md) em seu próprio ambiente de desenvolvimento.

Você pode saber mais sobre os números em C# nos seguintes artigos:

- [Tipos numéricos integrais](../../language-reference/builtin-types/integral-numeric-types.md)
- [Tipos numéricos de ponto flutuante](../../language-reference/builtin-types/floating-point-numeric-types.md)
- [Conversões numéricas internas](../../language-reference/builtin-types/numeric-conversions.md)
