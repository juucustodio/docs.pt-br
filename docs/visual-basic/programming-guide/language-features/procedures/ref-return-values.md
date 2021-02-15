---
description: 'Saiba mais sobre: suporte para valores de retorno de referência (Visual Basic)'
title: Valores de retorno de referência
ms.date: 04/28/2017
helpviewer_keywords:
- variables [Visual Basic]
- ref return values [Visual Basic]
- ref returns [Visual Basic]
ms.assetid: 5ef0cc69-eb3a-4a67-92a2-78585f223cb5
ms.openlocfilehash: 215a647c68eb7eadd394a1a7842ceb98c46e04a5
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100466543"
---
# <a name="support-for-reference-return-values-visual-basic"></a>Suporte para valores de retorno de referência (Visual Basic)

A partir do C# 7,0, a linguagem C# dá suporte a *valores de retorno de referência*. Uma maneira de entender os valores de retorno de referência é que eles são o oposto dos argumentos que são passados por referência a um método. Quando um argumento passado por referência é modificado, as alterações são refletidas no valor da variável no chamador. Quando um método fornece um valor de retorno de referência a um chamador, as modificações feitas no valor de retorno de referência pelo chamador são refletidas nos dados do método chamado.

Visual Basic não permite que você crie métodos com valores de retorno de referência, mas permite consumir valores de retorno de referência. Em outras palavras, você pode chamar um método com um valor de retorno de referência e modificar esse valor de retorno, e as alterações no valor de retorno de referência são refletidas nos dados do método chamado.

## <a name="modifying-the-ref-return-value-directly"></a>Modificando o valor de retorno de referência diretamente

Para métodos que sempre têm sucesso e não têm `ByRef` parâmetros, você pode modificar o valor de retorno de referência diretamente. Você pode fazer isso atribuindo o novo valor às expressões que retornam o valor de retorno de referência.

O exemplo C# a seguir define um `NumericValue.IncrementValue` método que incrementa um valor interno e o retorna como um valor de retorno de referência.

[!code-csharp[Ref-Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/procedures/ref-returns1.cs)]

O valor de retorno de referência é então modificado pelo chamador no exemplo a seguir Visual Basic. Observe que a linha com a `NumericValue.IncrementValue` chamada de método não atribui um valor ao método. Em vez disso, ele atribui um valor ao valor de retorno de referência retornado pelo método.

[!code-vb[Ref-Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/procedures/use-ref-returns1.vb)]

## <a name="using-a-helper-method"></a>Usando um método auxiliar

Em outros casos, modificar o valor de retorno de referência de uma chamada de método diretamente pode nem sempre ser desejável. Por exemplo, um método de pesquisa que retorna uma cadeia de caracteres nem sempre pode encontrar uma correspondência. Nesse caso, você deseja modificar o valor de retorno de referência somente se a pesquisa for bem-sucedida.

O exemplo C# a seguir ilustra esse cenário. Ele define uma `Sentence` classe escrita em C# que inclui um `FindNext` método que localiza a próxima palavra em uma frase que começa com uma subcadeia de caracteres especificada. A cadeia de caracteres é retornada como um valor retornado de referência e uma variável `Boolean` passada pela referência para o método indica se a pesquisa foi bem-sucedida. O valor de retorno de referência indica que, além de ler o valor retornado, o chamador também pode modificá-lo e essa modificação é refletida nos dados contidos internamente na `Sentence` classe.

[!code-csharp[Ref-Return](../../../../../samples/snippets/visualbasic/getting-started/ref-returns.cs)]

Modificar diretamente o valor de retorno de referência nesse caso não é confiável, pois a chamada do método pode falhar ao localizar uma correspondência e retornar a primeira palavra na sentença. Nesse caso, o chamador modificará inadvertidamente a primeira palavra da frase. Isso pode ser evitado pelo chamador que retorna um `null` (ou `Nothing` no Visual Basic). Mas nesse caso, tentar modificar uma cadeia de caracteres cujo valor é `Nothing` lança um <xref:System.NullReferenceException> . Se também puder ser impedido pelo chamador <xref:System.String.Empty?displayProperty=nameWithType> que retorna, mas isso exigirá que o chamador defina uma variável de cadeia de caracteres cujo valor seja <xref:System.String.Empty?displayProperty=nameWithType> . Embora o chamador possa modificar essa cadeia de caracteres, a modificação em si não atende a nenhuma finalidade, já que a cadeia de caracteres modificada não tem nenhuma relação com as palavras na sentença armazenada pela `Sentence` classe.

A melhor maneira de lidar com esse cenário é passar o valor de retorno de referência por referência a um método auxiliar. O método auxiliar, em seguida, contém a lógica para determinar se a chamada de método foi bem-sucedida e, se tiver feito, para modificar o valor de retorno de referência. O exemplo a seguir fornece uma implementação possível.

[!code-vb[Ref-Return](../../../../../samples/snippets/visualbasic/getting-started/ref-return-helper.vb#1)]

## <a name="see-also"></a>Consulte também

- [Passando argumentos por valor e por referência](passing-arguments-by-value-and-by-reference.md)
- [Procedimentos no Visual Basic](index.md)
