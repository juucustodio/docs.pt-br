---
title: Descartes – Guia do C#
description: Descreve o suporte do C# a descartes, que são variáveis descartáveis não atribuídas, além das maneiras em que descartes podem ser usados.
ms.technology: csharp-fundamentals
ms.date: 09/22/2020
ms.openlocfilehash: 7562da880ff3136dfc04ce4061bafa8ed55f5a23
ms.sourcegitcommit: 38999dc0ec4f7c4404de5ce0951b64c55997d9ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99426912"
---
# <a name="discards---c-guide"></a>Descartes – Guia do C#

A partir do C# 7,0, o C# dá suporte a Descartes, que são variáveis de espaço reservado que são intencionalmente não usadas no código do aplicativo. Os descartes são equivalentes a variáveis não atribuídas; Eles não têm um valor. Um descarte se comunica com a intenção do compilador e outros que lêem seu código: você pretende ignorar o resultado de uma expressão. Talvez você queira ignorar o resultado de uma expressão, um ou mais membros de uma expressão de tupla, um `out` parâmetro para um método ou o destino de uma expressão de correspondência de padrões.

Como há apenas uma única variável de descarte, essa variável talvez nem mesmo seja um armazenamento alocado. Os descartes podem reduzir as alocações de memória. Os descartes tornam a intenção do seu código claro. Eles aprimoram sua legibilidade e facilidade de manutenção.

Você indica que uma variável é um descarte atribuindo a ela o sublinhado (`_`) como seu nome. Por exemplo, a chamada de método a seguir retorna uma tupla na qual o primeiro e o segundo valores são descartados. `area` é uma variável previamente declarada definida para o terceiro componente retornado por `GetCityInformation` :

```csharp
(_, _, area) = city.GetCityInformation(cityName);
```

A partir do C# 9,0, você pode usar os descartes para especificar parâmetros de entrada não utilizados de uma expressão lambda. Para obter mais informações, consulte a seção [parâmetros de entrada de uma expressão lambda](language-reference/operators/lambda-expressions.md#input-parameters-of-a-lambda-expression) do artigo [expressões lambda](language-reference/operators/lambda-expressions.md) .

Quando `_` é um descarte válido, tentar recuperar seu valor ou usá-lo em uma operação de atribuição gera o erro de compilador CS0301, "o nome ' \_ ' não existe no contexto atual". Esse erro ocorre porque o `_` não recebe um valor e pode nem mesmo ser atribuído a um local de armazenamento. Se fosse uma variável real, você não poderia descartar mais de um valor, como fazia o exemplo anterior.

## <a name="tuple-and-object-deconstruction"></a>Desconstrução de objeto e de tupla

Os descartes são úteis para trabalhar com tuplas quando o código do aplicativo usa alguns elementos de tupla, mas ignora outros. Por exemplo, o método a seguir `QueryCityDataForYears` retorna uma tupla com o nome de uma cidade, sua área, um ano, a população da cidade para esse ano, um segundo ano e a população da cidade para esse segundo ano. O exemplo mostra a alteração na população entre esses dois anos. Entre os dados disponíveis da tupla, não estamos preocupados com a área da cidade e sabemos o nome da cidade e as duas datas em tempo de design. Como resultado, estamos interessados apenas nos dois valores de população armazenados na tupla e podemos lidar com seus valores restantes como descartes.  

:::code language="csharp" source="snippets/discards/discard-tuple.cs" ID="DiscardTupleMember" :::

Para obter mais informações sobre desconstruir tuplas com descartes, consulte [Desconstruindo tuplas e outros tipos](deconstruct.md#deconstructing-tuple-elements-with-discards).

O método `Deconstruct` de uma classe, estrutura ou interface também permite que você recupere e decomponha um conjunto específico de dados de um objeto. Você pode usar os descartes quando estiver interessado em trabalhar com apenas um subconjunto dos valores desconstruídos. O exemplo a seguir desconstrói um objeto `Person` em quatro cadeias de caracteres (os nomes e sobrenomes, a cidade e o estado), mas descarta o sobrenome e o estado.

:::code language="csharp" source="snippets/discards/discard-class.cs" :::

Para obter mais informações sobre desconstruir tipos definidos pelo usuário com descartes, consulte [Desconstruindo tuplas e outros tipos](deconstruct.md#deconstructing-a-user-defined-type-with-discards).

## <a name="pattern-matching-with-switch"></a>Correspondência de padrões com ' switch '

O *padrão de descarte* pode ser usado na correspondência de padrões com a palavra-chave [switch](language-reference/keywords/switch.md) . Toda expressão sempre corresponde ao padrão de descarte. (Ele pode ser usado com expressões [is](language-reference/keywords/is.md) . No entanto, esse uso é raro porque o descarte pode ser removido sem alterar seu significado).

O exemplo a seguir define um método `ProvidesFormatInfo` que usa instruções [is](language-reference/keywords/is.md) para determinar se um objeto fornece uma implementação de <xref:System.IFormatProvider> e testa se o objeto é `null`. Ele também usa o padrão de descarte para manipular objetos não nulos de qualquer outro tipo.

:::code language="csharp" source="snippets/discards/discard-pattern2.cs" ID="DiscardSwitchExample" :::

## <a name="calls-to-methods-with-out-parameters"></a>Chamadas para métodos com `out` parâmetros

Ao chamar o método `Deconstruct` para desconstruir um tipo definido pelo usuário (uma instância de uma classe, estrutura ou interface), você pode descartar os valores de argumentos `out` individuais. Mas você também pode descartar o valor de `out` argumentos ao chamar qualquer método com um `out` parâmetro.

A exemplo a seguir chama o método [DateTime.TryParse(String, out DateTime)](<xref:System.DateTime.TryParse(System.String,System.DateTime@)>) para determinar se a representação de cadeia de caracteres de uma data é válida na cultura atual. Já que o exemplo está preocupado apenas em validar a cadeia de caracteres de data e não em analisá-lo para extrair a data, o argumento `out` para o método é um descarte.

:::code language="csharp" source="snippets/discards/discard-out1.cs" ID="DiscardOutParameter" :::

## <a name="a-standalone-discard"></a>Um descarte autônomo

Você pode usar um descarte autônomo para indicar qualquer variável que você opte por ignorar. Um uso típico é usar uma atribuição para garantir que um argumento não seja nulo. O código a seguir usa um descarte para forçar uma atribuição. O lado direito da atribuição usa o [operador de União nulo](language-reference/operators/null-coalescing-operator.md) para gerar um <xref:System.ArgumentNullException?displayProperty=nameWithType> quando o argumento é `null` . O código não precisa do resultado da atribuição e, portanto, é Descartado. A expressão força uma verificação nula. O descarte esclarece sua intenção: o resultado da atribuição não é necessário ou usado.

:::code language="csharp" source="snippets/discards/standalone-discard1.cs" ID="ArgNullCheck" :::

O exemplo a seguir usa um descarte autônomo para ignorar o objeto <xref:System.Threading.Tasks.Task> retornado por uma operação assíncrona. A atribuição da tarefa tem o efeito de suprimir a exceção que a operação gera, pois ela está prestes a ser concluída. Isso torna sua intenção clara: você deseja descartar o `Task` e ignorar todos os erros gerados dessa operação assíncrona.

:::code language="csharp" source="snippets/discards/standalone-discard1.cs" ID="SnippetDiscardTask" :::

Sem atribuir a tarefa a um descarte, o código a seguir gera um aviso do compilador:

:::code language="csharp" source="snippets/discards/standalone-discard1.cs" ID="SnippetNoDiscardTask" :::

> [!NOTE]
> Se você executar qualquer um dos dois exemplos anteriores usando um depurador, o depurador interromperá o programa quando a exceção for lançada. Sem um depurador anexado, a exceção é silenciosamente ignorada em ambos os casos.

`_` também é um identificador válido. Quando usado fora de um contexto com suporte, `_` não é tratado como um descarte, mas como uma variável válida. Se um identificador chamado `_` já está no escopo, o uso de `_` como um descarte autônomo pode resultar em:

- A modificação acidental do valor da variável `_` no escopo atribuindo a ela o valor do descarte pretendido. Por exemplo:
   :::code language="csharp" source="snippets/discards/standalone-discard2.cs" ID="VariableIdentifier" :::
- Um erro do compilador por violação de segurança de tipo. Por exemplo:
   :::code language="csharp" source="snippets/discards/standalone-discard2.cs" ID="VariableTypeInference" :::
- Erro do compilador CS0136, "Um local ou um parâmetro denominado '\_' não pode ser declarado neste escopo porque esse nome é usado em um escopo delimitador de local para definir um local ou parâmetro." Por exemplo:
   :::code language="csharp" source="snippets/discards/standalone-discard2.cs" ID="CannotRedeclare" :::

## <a name="see-also"></a>Confira também

- [Desconstruindo tuplas e outros tipos](deconstruct.md)
- [`is` chaves](language-reference/keywords/is.md)
- [`switch` chaves](language-reference/keywords/switch.md)
