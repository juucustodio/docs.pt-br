---
title: com expressão-referência C#
description: Saiba mais sobre uma expressão with que executa mutação não destrutiva de registros C#
ms.date: 11/12/2020
f1_keywords:
- with_CSharpKeyword
helpviewer_keywords:
- with expression [C#]
- with operator [C#]
ms.openlocfilehash: d7d3758c8c5da7859974b5b50b63d2a5ca16b24d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95702219"
---
# <a name="with-expression-c-reference"></a>expressão with (referência C#)

Disponível em C# 9,0 e posterior, uma `with` expressão produz uma cópia de seu operando de [registro](../../whats-new/csharp-9.md#record-types) com as propriedades e os campos especificados modificados:

:::code language="csharp" source="snippets/with-expression/BasicExample.cs" :::

Como mostra o exemplo anterior, você usa a sintaxe do [inicializador de objeto](../../programming-guide/classes-and-structs/object-and-collection-initializers.md) para especificar quais membros modificar e seus novos valores. Em uma `with` expressão, um operando à esquerda deve ser de um tipo de registro.

O resultado de uma `with` expressão tem o mesmo tipo de tempo de execução que o operando da expressão, como mostra o exemplo a seguir:

:::code language="csharp" source="snippets/with-expression/InheritanceExample.cs" :::

No caso de um membro de tipo de referência, somente a referência a uma instância é copiada quando um registro é copiado. A cópia e o registro original têm acesso à mesma instância de tipo de referência. O exemplo a seguir demonstra esse comportamento:

:::code language="csharp" source="snippets/with-expression/ExampleWithReferenceType.cs" :::

Qualquer tipo de registro tem o *Construtor de cópia*. Esse é um construtor com um único parâmetro do tipo de registro que o contém. Ele copia o estado de seu argumento para uma nova instância de registro. Na avaliação de uma `with` expressão, o construtor de cópia é chamado para instanciar uma nova instância de registro com base em um registro original. Depois disso, a nova instância é atualizada de acordo com as modificações especificadas. Por padrão, o construtor de cópia é implícito, ou seja, gerado pelo compilador. Se você precisar personalizar a semântica de cópia de registro, declare explicitamente um construtor de cópia com o comportamento desejado. O exemplo a seguir atualiza o exemplo anterior com um construtor de cópia explícito. O novo comportamento de cópia é copiar itens de lista em vez de uma referência de lista quando um registro é copiado:

:::code language="csharp" source="snippets/with-expression/UserDefinedCopyConstructor.cs" :::

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, consulte as seções a seguir da [proposta de recurso de registros observação](~/_csharplang/proposals/csharp-9.0/records.md):

- [`with` expressão](~/_csharplang/proposals/csharp-9.0/records.md#with-expression)
- [Copiar e clonar Membros](~/_csharplang/proposals/csharp-9.0/records.md#copy-and-clone-members)

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Operadores e expressões C#](index.md)
