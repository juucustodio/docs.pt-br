---
description: 'Saiba mais sobre: como armazenar mais de um valor em uma variável (Visual Basic)'
title: 'Como: Manter mais de um valor em uma variável'
ms.date: 07/20/2015
helpviewer_keywords:
- classes [Visual Basic], composite data types
- composite types [Visual Basic]
- composite data types [Visual Basic]
- data types [Visual Basic], composite
- arrays [Visual Basic], composite data types
- structures [Visual Basic], composite data types
- arrays [Visual Basic], compilation errors
- types [Visual Basic], composite
ms.assetid: 5fe0e558-aac2-4a40-b7f2-7cfea7336917
ms.openlocfilehash: 5248bc29f58cccf3b8ced95d3fba8f0d39033a83
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100483996"
---
# <a name="how-to-hold-more-than-one-value-in-a-variable-visual-basic"></a>Como manter mais de um valor em uma variável (Visual Basic)

Uma variável contém mais de um valor se você declará-lo para ser de um *tipo de dados composto*.

[Os tipos de dados compostos](composite-data-types.md) incluem estruturas, matrizes e classes. Uma variável de um tipo de dados de composição pode conter uma combinação de tipos de dados elementares e outros tipos compostos. Estruturas e classes podem conter código, bem como dados.

## <a name="to-hold-more-than-one-value-in-a-variable"></a>Para conter mais de um valor em uma variável

1. Determine o tipo de dados composto que você deseja usar para a variável.

2. Se o tipo de dados composto ainda não estiver definido, defina-o para que sua variável possa usá-lo.

    - Defina uma estrutura com uma [instrução de estrutura](../../../language-reference/statements/structure-statement.md).

    - Defina uma matriz com uma [instrução Dim](../../../language-reference/statements/dim-statement.md).

    - Defina uma classe com uma [instrução de classe](../../../language-reference/statements/class-statement.md).

3. Declare sua variável com uma `Dim` instrução.

4. Siga o nome da variável com uma `As` cláusula.

5. Siga a `As` palavra-chave com o nome do tipo de dados composto apropriado.

## <a name="see-also"></a>Consulte também

- [Data Types](../../../language-reference/data-types/index.md)
- [Caracteres de tipo](type-characters.md)
- [Tipos de dados compostos](composite-data-types.md)
- [Estruturas](structures.md)
- [matrizes](../arrays/index.md)
- [Objetos e classes](../objects-and-classes/index.md)
- [Tipos de valor e tipos de referência](value-types-and-reference-types.md)
