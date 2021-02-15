---
description: 'Saiba mais sobre: tipos de valores anuláveis (Visual Basic)'
title: Tipos de valor anuláveis
ms.date: 07/20/2015
f1_keywords:
- vb.Nullable
helpviewer_keywords:
- nullable types [Visual Basic]
- '? [Visual Basic]'
- types [Visual Basic], nullable
- nullable types [Visual Basic]
- data types [Visual Basic], nullable
ms.assetid: 9ac3b602-6f96-4e6d-96f7-cd4e81c468a6
ms.openlocfilehash: acc91d98a3ed288a9bf0bcf6abbd3d8a516bd699
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100483879"
---
# <a name="nullable-value-types-visual-basic"></a>Tipos de valor que permitem valor nulo (Visual Basic)

Às vezes, você trabalha com um tipo de valor que não tem um valor definido em determinadas circunstâncias. Por exemplo, um campo em um banco de dados pode ter que distinguir entre ter um valor atribuído que seja significativo e não tenha um valor atribuído. Os tipos de valor podem ser estendidos para obter seus valores normais ou um valor nulo. Essa extensão é chamada de *tipo anulável*.

Cada tipo de valor anulável é construído a partir da <xref:System.Nullable%601> estrutura genérica. Considere um banco de dados que controla atividades relacionadas ao trabalho. O exemplo a seguir constrói um `Boolean` tipo anulável e declara uma variável desse tipo. Você pode escrever a declaração de três maneiras:

[!code-vb[VbVbalrNullableValue#1](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#1)]

A variável `ridesBusToWork` pode conter um valor `True` , um valor `False` ou nenhum valor. Seu valor padrão inicial não é nenhum valor, que nesse caso pode significar que as informações ainda não foram obtidas para essa pessoa. Por outro lado, `False` pode significar que as informações foram obtidas e a pessoa não pode fazer o barramento funcionar.

Você pode declarar variáveis e propriedades com tipos de valor anulável e pode declarar uma matriz com elementos de um tipo de valor anulável. Você pode declarar procedimentos com tipos de valor anuláveis como parâmetros e pode retornar um tipo de valor anulável de um `Function` procedimento.

Você não pode construir um tipo anulável em um tipo de referência, como uma matriz, uma `String` ou uma classe. O tipo subjacente deve ser um tipo de valor. Para obter mais informações, consulte [tipos de valor e tipos de referência](value-types-and-reference-types.md).

## <a name="using-a-nullable-type-variable"></a>Usando uma variável de tipo anulável

Os membros mais importantes de um tipo de valor anulável são <xref:System.Nullable%601.HasValue%2A> suas <xref:System.Nullable%601.Value%2A> Propriedades e. Para uma variável de um tipo de valor anulável, <xref:System.Nullable%601.HasValue%2A> informa se a variável contém um valor definido. Se <xref:System.Nullable%601.HasValue%2A> for `True` , você poderá ler o valor de <xref:System.Nullable%601.Value%2A> . Observe que <xref:System.Nullable%601.HasValue%2A> e <xref:System.Nullable%601.Value%2A> são `ReadOnly` Propriedades.

### <a name="default-values"></a>Valores padrão

Quando você declara uma variável com um tipo de valor anulável, sua <xref:System.Nullable%601.HasValue%2A> propriedade tem um valor padrão de `False` . Isso significa que, por padrão, a variável não tem nenhum valor definido, em vez do valor padrão de seu tipo de valor subjacente. No exemplo a seguir, a variável `numberOfChildren` inicialmente não tem nenhum valor definido, embora o valor padrão do `Integer` tipo seja 0.

[!code-vb[VbVbalrNullableValue#2](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#2)]

Um valor nulo é útil para indicar um valor indefinido ou desconhecido. Se `numberOfChildren` tivesse sido declarado como `Integer` , não haveria nenhum valor que possa indicar que as informações não estão disponíveis no momento.

### <a name="storing-values"></a>Armazenando valores

Você armazena um valor em uma variável ou propriedade de um tipo de valor anulável da maneira típica. O exemplo a seguir atribui um valor à variável `numberOfChildren` declarada no exemplo anterior.

[!code-vb[VbVbalrNullableValue#3](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#3)]

Se uma variável ou propriedade de um tipo de valor anulável contiver um valor definido, você poderá fazer com que ele reverta para seu estado inicial de não ter um valor atribuído. Você faz isso definindo a variável ou a propriedade como `Nothing` , como mostra o exemplo a seguir.

[!code-vb[VbVbalrNullableValue#4](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#4)]

> [!NOTE]
> Embora você possa atribuir `Nothing` a uma variável de um tipo de valor anulável, não é possível testá-lo para `Nothing` o usando o sinal de igual. Comparação que usa o sinal de igual, `someVar = Nothing` , sempre é avaliada como `Nothing` . Você pode testar a propriedade da variável <xref:System.Nullable%601.HasValue%2A> para `False` ou testar usando o `Is` `IsNot` operador OR.

### <a name="retrieving-values"></a>Recuperando valores

Para recuperar o valor de uma variável de um tipo de valor anulável, você deve primeiro testar sua <xref:System.Nullable%601.HasValue%2A> propriedade para confirmar que ela tem um valor. Se você tentar ler o valor quando <xref:System.Nullable%601.HasValue%2A> for `False` , Visual Basic lançará uma <xref:System.InvalidOperationException> exceção. O exemplo a seguir mostra a maneira recomendada para ler a variável `numberOfChildren` dos exemplos anteriores.

[!code-vb[VbVbalrNullableValue#5](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#5)]

## <a name="comparing-nullable-types"></a>Comparando tipos anuláveis

Quando variáveis anuláveis `Boolean` são usadas em expressões booleanas, o resultado pode ser `True` , `False` ou `Nothing` . A seguir, a tabela verdade para o `And` e o `Or` . Como `b1` e `b2` agora tem três valores possíveis, há nove combinações a serem avaliadas.

|B1|B2|B1 e B2|B1 ou B2|
|--------|--------|---------------|--------------|
|`Nothing`|`Nothing`|`Nothing`|`Nothing`|
|`Nothing`|`True`|`Nothing`|`True`|
|`Nothing`|`False`|`False`|`Nothing`|
|`True`|`Nothing`|`Nothing`|`True`|
|`True`|`True`|`True`|`True`|
|`True`|`False`|`False`|`True`|
|`False`|`Nothing`|`False`|`Nothing`|
|`False`|`True`|`False`|`True`|
|`False`|`False`|`False`|`False`|

Quando o valor de uma variável ou expressão booliana é `Nothing` , não é `true` nem `false` . Considere o exemplo a seguir.

[!code-vb[VbVbalrNullableValue#6](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#6)]

Neste exemplo, `b1 And b2` é avaliado como `Nothing` . Como resultado, a `Else` cláusula é executada em cada `If` instrução e a saída é a seguinte:

`Expression is not true`

`Expression is not false`

> [!NOTE]
> `AndAlso` e `OrElse` , que usam a avaliação de curto-circuito, devem avaliar seus segundo operandos quando o primeiro é avaliado como `Nothing` .

## <a name="propagation"></a>Propagação

Se um ou ambos os operandos de uma operação aritmética, de comparação, de deslocamento ou de tipo for um tipo de valor anulável, o resultado da operação também será um tipo de valor anulável. Se ambos os operandos tiverem valores que não são `Nothing` , a operação será executada nos valores subjacentes dos operandos, como se nenhum deles fosse um tipo de valor anulável. No exemplo a seguir, as variáveis `compare1` e `sum1` são digitadas implicitamente. Se você posicionar o ponteiro do mouse sobre eles, verá que o compilador infere os tipos de valores anuláveis para ambos.

[!code-vb[VbVbalrNullableValue#7](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#7)]

Se um ou ambos os operandos tiverem um valor de `Nothing` , o resultado será `Nothing` .

[!code-vb[VbVbalrNullableValue#8](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#8)]

## <a name="using-nullable-types-with-data"></a>Usando tipos anuláveis com dados

Um banco de dados é um dos lugares mais importantes para usar tipos de valor anulável. Nem todos os objetos de banco de dados dão suporte atualmente a tipos de valor anuláveis, mas os adaptadores de tabela gerados pelo designer fazem. Consulte [suporte do TableAdapter para tipos anuláveis](/visualstudio/data-tools/fill-datasets-by-using-tableadapters#tableadapter-support-for-nullable-types).

## <a name="see-also"></a>Consulte também

- <xref:System.InvalidOperationException>
- <xref:System.Nullable%601.HasValue%2A>
- [Data Types](index.md)
- [Tipos de valor e tipos de referência](value-types-and-reference-types.md)
- [Solução de problemas de tipos de dados](troubleshooting-data-types.md)
- [Preencher conjuntos de dados usando TableAdapters](/visualstudio/data-tools/fill-datasets-by-using-tableadapters)
- [Operador If](../../../language-reference/operators/if-operator.md)
- [Inferência de Tipo de Variável Local](../variables/local-type-inference.md)
- [Operador Is](../../../language-reference/operators/is-operator.md)
- [Operador IsNot](../../../language-reference/operators/isnot-operator.md)
- [Tipos de valor anulável (C#)](../../../../csharp/language-reference/builtin-types/nullable-value-types.md)
