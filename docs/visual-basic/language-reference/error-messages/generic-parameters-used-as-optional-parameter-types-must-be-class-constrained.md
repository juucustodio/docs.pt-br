---
description: 'Saiba mais sobre: BC32124: parâmetros genéricos usados como tipos de parâmetro opcionais devem ser restritos por classe'
title: Parâmetros genéricos usados como tipos de parâmetro opcionais devem ter a classe restrita
ms.date: 07/20/2015
f1_keywords:
- vbc32124
- bc32124
helpviewer_keywords:
- BC32124
ms.assetid: 55aa8b2a-9ce3-4620-a710-2f9b0feb6143
ms.openlocfilehash: 0014720d55dc4395178186b5e183d5b0279d7029
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796139"
---
# <a name="bc32124-generic-parameters-used-as-optional-parameter-types-must-be-class-constrained"></a>BC32124: parâmetros genéricos usados como tipos de parâmetro opcionais devem ser restritos por classe

Um procedimento é declarado com um parâmetro opcional que usa um parâmetro de tipo que não é restrito a ser um tipo de referência.

 Você sempre deve fornecer um valor padrão para cada parâmetro opcional. Se o parâmetro for de um tipo de referência, o valor opcional deverá ser `Nothing` , que é um valor válido para qualquer tipo de referência. No entanto, se o parâmetro for de um tipo de valor, esse tipo deverá ser um tipo de dados elementar predefinido por Visual Basic. Isso ocorre porque um tipo de valor composto, como uma estrutura definida pelo usuário, não tem um valor padrão válido.

 Quando você usa um parâmetro de tipo para um parâmetro opcional, você deve garantir que ele seja de um tipo de referência para evitar a possibilidade de um tipo de valor sem um valor padrão válido. Isso significa que você deve restringir o parâmetro de tipo com a `Class` palavra-chave ou com o nome de uma classe específica.

 **ID do erro:** BC32124

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Restrinja o parâmetro de tipo para aceitar apenas um tipo de referência ou não use-o para o parâmetro opcional.

## <a name="see-also"></a>Consulte também

- [Tipos genéricos no Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [Lista de Tipos](../statements/type-list.md)
- [Instrução Class](../statements/class-statement.md)
- [Parâmetros Opcionais](../../programming-guide/language-features/procedures/optional-parameters.md)
- [Estruturas](../../programming-guide/language-features/data-types/structures.md)
- [Nothing](../nothing.md)
