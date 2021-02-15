---
description: '! operador (NULL-tolerante)-referência C#'
title: '! operador (NULL-tolerante)-referência C#'
ms.date: 11/13/2020
f1_keywords:
- nullForgiving_CSharpKeyword
helpviewer_keywords:
- null-forgiving operator [C#]
- '! operator [C#]'
ms.openlocfilehash: 7b8c634404cf2f214cc4bee5d754443e9302a723
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739510"
---
# <a name="-null-forgiving-operator-c-reference"></a>! operador (NULL-tolerante) (referência C#)

Disponível em C# 8,0 e posterior, o operador de sufixo unário `!` é o operador NULL-tolerante ou NULL-supressão. Em um [contexto de anotação anulável](../../nullable-references.md#nullable-annotation-context)habilitado, você usa o operador NULL-tolerante para declarar que a expressão `x` de um tipo de referência não é `null` : `x!` . O operador de prefixo unário `!` é o [operador lógico de negação](boolean-logical-operators.md#logical-negation-operator-).

O operador NULL-tolerante não tem nenhum efeito no tempo de execução. Ele afeta apenas a análise de fluxo estático do compilador, alterando o estado nulo da expressão. Em tempo de execução, `x!` a expressão é avaliada como o resultado da expressão subjacente `x` .

Para obter mais informações sobre o recurso de tipos de referência anulável, consulte [tipos de referência anuláveis](../builtin-types/nullable-reference-types.md).

## <a name="examples"></a>Exemplos

Um dos casos de uso do operador NULL-tolerante está no teste da lógica de validação de argumento. Por exemplo, considere a seguinte classe:

[!code-csharp[Person class](snippets/shared/NullForgivingOperator.cs#PersonClass)]

Usando a [estrutura de teste MSTest](../../../core/testing/unit-testing-with-mstest.md), você pode criar o seguinte teste para a lógica de validação no construtor:

[!code-csharp[Person test](snippets/shared/NullForgivingOperator.cs#TestPerson)]

Sem o operador NULL-tolerante, o compilador gera o seguinte aviso para o código anterior: `Warning CS8625: Cannot convert null literal to non-nullable reference type` . Usando o operador NULL-tolerante, você informa ao compilador que a passagem `null` é esperada e não deve ser avisado sobre.

Você também pode usar o operador NULL-tolerante quando sabe definitivamente que uma expressão não pode ser `null` , mas o compilador não gerencia para reconhecê-la. No exemplo a seguir, se o `IsValid` método retornar `true` , seu argumento não será `null` e você poderá desreferenciá-lo com segurança:

[!code-csharp[Use null-forgiving operator](snippets/shared/NullForgivingOperator.cs#UseNullForgiving)]

Sem o operador NULL-tolerante, o compilador gera o seguinte aviso para o `p.Name` código: `Warning CS8602: Dereference of a possibly null reference` .

Se você puder modificar o `IsValid` método, poderá usar o atributo [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute) para informar ao compilador que um argumento do `IsValid` método não pode ser `null` quando o método retornar `true` :

[!code-csharp[Use an attribute](snippets/shared/NullForgivingOperator.cs#UseAttribute)]

No exemplo anterior, você não precisa usar o operador NULL-tolerante porque o compilador tem informações suficientes para descobrir que `p` não podem estar `null` dentro da `if` instrução. Para obter mais informações sobre os atributos que permitem fornecer informações adicionais sobre o estado nulo de uma variável, consulte [Atualizar APIs com atributos para definir expectativas nulas](../attributes/nullable-analysis.md).

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, consulte [a seção operador NULL-tolerante](~/_csharplang/proposals/csharp-9.0/nullable-reference-types-specification.md#the-null-forgiving-operator) do [rascunho da especificação de tipos de referência anulável](~/_csharplang/proposals/csharp-9.0/nullable-reference-types-specification.md).

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Operadores e expressões C#](index.md)
- [Tutorial: design com tipos de referência anuláveis](../../tutorials/nullable-reference-types.md)
