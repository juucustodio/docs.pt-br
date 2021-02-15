---
title: Movendo árvores de expressão
description: Aprenda a visitar cada nó em uma árvore de expressão, enquanto estiver criando uma cópia modificada dessa árvore de expressão.
ms.date: 06/20/2016
ms.technology: csharp-advanced-concepts
ms.assetid: b453c591-acc6-4e08-8175-97e5bc65958e
ms.openlocfilehash: cb64e79d915a5c5567d5a3d25f1d747df9687c87
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537457"
---
# <a name="translate-expression-trees"></a>Traduzir árvores de expressões

[Anterior – Compilando expressões](expression-trees-building.md)

Nesta seção final, você aprenderá a visitar cada nó em uma árvore de expressão, enquanto estiver criando uma cópia modificada dessa árvore de expressão. Essas são as técnicas que você usará em dois cenários importantes. O primeiro é entender os algoritmos expressados por uma árvore de expressão para que ela possa ser movida para outro ambiente. O segundo é quando você deseja alterar o algoritmo que foi criado. Isso poderia ser feito para adicionar registro em log, interceptar chamadas de método e monitorá-las ou outras finalidades.

## <a name="translating-is-visiting"></a>Mover é visitar

O código que você compila para mover uma árvore de expressão é uma extensão do que você já viu para visitar todos os nós em uma árvore. Quando você move uma árvore de expressão, visita todos os nós e ao visitá-los, cria a nova árvore. A nova árvore pode conter referências aos nós originais ou aos novos nós que você colocou na árvore.

Vamos ver isso em ação, visitando uma árvore de expressão e criando uma nova árvore com alguns nós de substituição. Neste exemplo, vamos substituir qualquer constante com uma constante que seja dez vezes maior.
Caso contrário, vamos deixar a árvore de expressão intacta. Em vez de ler o valor da constante e substituí-la por uma nova constante, faremos essa substituição através da troca do nó constante por um novo nó que executa a multiplicação.

Aqui, quando você encontrar um nó constante, você criará um novo nó de multiplicação cujos filhos serão a constante original e a constante `10`:

```csharp
private static Expression ReplaceNodes(Expression original)
{
    if (original.NodeType == ExpressionType.Constant)
    {
        return Expression.Multiply(original, Expression.Constant(10));
    }
    else if (original.NodeType == ExpressionType.Add)
    {
        var binaryExpression = (BinaryExpression)original;
        return Expression.Add(
            ReplaceNodes(binaryExpression.Left),
            ReplaceNodes(binaryExpression.Right));
    }
    return original;
}
```

Ao substituir o nó original pelo substituto, uma nova árvore será formada, contendo as nossas modificações. Podemos verificar isso compilando e executando a árvore substituída.

```csharp
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var addition = Expression.Add(one, two);
var sum = ReplaceNodes(addition);
var executableFunc = Expression.Lambda(sum);

var func = (Func<int>)executableFunc.Compile();
var answer = func();
Console.WriteLine(answer);
```

A criação de uma nova árvore é uma combinação da visita aos nós da árvore existentes e a criação de novos nós, inserindo-os na árvore.

Este exemplo mostra a importância das árvores de expressão serem imutáveis. Observe que a nova árvore criada acima contém uma mistura de nós recém-criados e nós da árvore existente. E isso é seguro, porque os nós da árvore existente não podem ser modificados. Isso pode resultar em eficiências significativas de memória.
Os mesmos nós podem ser usados em toda a árvore ou em várias árvores de expressão. Como os nós não podem ser modificados, o mesmo nó pode ser reutilizado sempre que necessário.

## <a name="traversing-and-executing-an-addition"></a>Percorrer e executar uma adição

Vamos verificar isso criando um segundo visitante que percorre a árvore de nós de adição e calcula o resultado. Você pode fazer isso com algumas modificações no visitante que utilizamos até agora. Nessa nova versão, o visitante retornará a soma parcial da operação de adição até este ponto. Para uma expressão constante, esse é simplesmente o valor da expressão constante. Para uma expressão de adição, o resultado será a soma dos operandos esquerdos e direitos, uma vez que essas árvores forem percorridas.

```csharp
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var three= Expression.Constant(3, typeof(int));
var four = Expression.Constant(4, typeof(int));
var addition = Expression.Add(one, two);
var add2 = Expression.Add(three, four);
var sum = Expression.Add(addition, add2);

// Declare the delegate, so we can call it
// from itself recursively:
Func<Expression, int> aggregate = null;
// Aggregate, return constants, or the sum of the left and right operand.
// Major simplification: Assume every binary expression is an addition.
aggregate = (exp) =>
    exp.NodeType == ExpressionType.Constant ?
    (int)((ConstantExpression)exp).Value :
    aggregate(((BinaryExpression)exp).Left) + aggregate(((BinaryExpression)exp).Right);

var theSum = aggregate(sum);
Console.WriteLine(theSum);
```

Tem bastante código nisso, mas os conceitos são bastante acessíveis.
Esse código visita filhos em uma pesquisa de profundidade inicial. Ao encontrar um nó constante, o visitante retorna o valor da constante. Depois que o visitante visitar ambos os filhos, esses filhos terão calculado a soma calculada para essa subárvore. Agora o nó de adição poderá computar sua soma.
Uma vez que todos os nós da árvore de expressão forem visitados, a soma será calculada. Você pode executar o exemplo no depurador e rastrear a execução.

Vamos facilitar o rastreamento de como os nós são analisados e como a soma é calculada, percorrendo a árvore. Esta é uma versão atualizada do método de agregação que inclui bastante informação de rastreamento:

```csharp
private static int Aggregate(Expression exp)
{
    if (exp.NodeType == ExpressionType.Constant)
    {
        var constantExp = (ConstantExpression)exp;
        Console.Error.WriteLine($"Found Constant: {constantExp.Value}");
        return (int)constantExp.Value;
    }
    else if (exp.NodeType == ExpressionType.Add)
    {
        var addExp = (BinaryExpression)exp;
        Console.Error.WriteLine("Found Addition Expression");
        Console.Error.WriteLine("Computing Left node");
        var leftOperand = Aggregate(addExp.Left);
        Console.Error.WriteLine($"Left is: {leftOperand}");
        Console.Error.WriteLine("Computing Right node");
        var rightOperand = Aggregate(addExp.Right);
        Console.Error.WriteLine($"Right is: {rightOperand}");
        var sum = leftOperand + rightOperand;
        Console.Error.WriteLine($"Computed sum: {sum}");
        return sum;
    }
    else throw new NotSupportedException("Haven't written this yet");
}
```

Executá-lo na mesma expressão produz o seguinte resultado:

```output
10
Found Addition Expression
Computing Left node
Found Addition Expression
Computing Left node
Found Constant: 1
Left is: 1
Computing Right node
Found Constant: 2
Right is: 2
Computed sum: 3
Left is: 3
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 3
Left is: 3
Computing Right node
Found Constant: 4
Right is: 4
Computed sum: 7
Right is: 7
Computed sum: 10
10
```

Rastreie a saída e acompanhe no código acima. Você será capaz de entender como o código visita cada nó e calcula a soma, à medida que percorre a árvore e localiza a soma.

Agora, vejamos uma execução diferente, com a expressão fornecida por `sum1`:

```csharp
Expression<Func<int> sum1 = () => 1 + (2 + (3 + 4));
```

Aqui está a saída ao examinar essa expressão:

```output
Found Addition Expression
Computing Left node
Found Constant: 1
Left is: 1
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 2
Left is: 2
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 3
Left is: 3
Computing Right node
Found Constant: 4
Right is: 4
Computed sum: 7
Right is: 7
Computed sum: 9
Right is: 9
Computed sum: 10
10
```

Embora a resposta final seja a mesma, a forma de percorrer a árvore é completamente diferente. Os nós são percorridos em uma ordem diferente, porque a árvore foi construída com operações diferentes que ocorrem primeiro.

## <a name="learning-more"></a>Para saber mais

Este exemplo mostra um pequeno subconjunto do código que você compilaria para percorrer e interpretar os algoritmos representados por uma árvore de expressão. Para obter uma discussão completa a respeito de todo o trabalho necessário para compilar uma biblioteca de finalidade geral que move árvores de expressão para outra linguagem, leia [esta série](/archive/blogs/mattwar/linq-building-an-iqueryable-provider-series) escrita por Matt Warren. Ele entra em detalhes de como mover qualquer código que você pode encontrar em uma árvore de expressão.

Espero que você tenha visto o verdadeiro poder das árvores de expressão.
Você pode examinar um conjunto de códigos, fazer as alterações que desejar nesse código e executar a versão modificada. Como as árvores de expressão são imutáveis, você pode criar novas árvores usando os componentes de árvores existentes. Isso minimiza a quantidade de memória necessária para criar árvores de expressão modificadas.

[Próximo – Resumindo](expression-trees-summary.md)
