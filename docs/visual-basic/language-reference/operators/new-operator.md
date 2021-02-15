---
description: 'Saiba mais sobre: novo operador (Visual Basic)'
title: Operador New
ms.date: 07/20/2015
f1_keywords:
- vb.new
- vb.NewConstraint
helpviewer_keywords:
- constraints, Visual Basic generic types
- generics [Visual Basic], constraints
- constraints, New keyword [Visual Basic]
- New constraint
- New keyword [Visual Basic]
ms.assetid: d7d566d7-fe0e-4336-91f7-641a542de4d0
ms.openlocfilehash: f52dd7606127c7587173de8a78e618ceb3e4681d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99665374"
---
# <a name="new-operator-visual-basic"></a>Operador New (Visual Basic)

Apresenta uma `New` cláusula para criar uma nova instância de objeto, especifica uma restrição de Construtor em um parâmetro de tipo ou identifica um `Sub` procedimento como um construtor de classe.

## <a name="remarks"></a>Comentários

Em uma declaração ou instrução de atribuição, uma `New` cláusula deve especificar uma classe definida da qual a instância pode ser criada. Isso significa que a classe deve expor um ou mais construtores que o código de chamada pode acessar.

Você pode usar uma `New` cláusula em uma instrução de declaração ou uma instrução de atribuição. Quando a instrução é executada, ela chama o construtor apropriado da classe especificada, passando os argumentos que você forneceu. O exemplo a seguir demonstra isso criando instâncias de uma `Customer` classe que tem dois construtores, um que não usa parâmetros e um que usa um parâmetro de cadeia de caracteres:

[!code-vb[VbVbalrKeywords#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class6.vb#11)]

Como as matrizes são classes, `New` o pode criar uma nova instância de matriz, conforme mostrado no exemplo a seguir:

[!code-vb[VbVbalrKeywords#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class6.vb#12)]

O Common Language Runtime (CLR) gera um <xref:System.OutOfMemoryException> erro se não houver memória suficiente para criar a nova instância.

> [!NOTE]
> A `New` palavra-chave também é usada em listas de parâmetros de tipo para especificar que o tipo fornecido deve expor um construtor acessível sem parâmetros. Para obter mais informações sobre parâmetros de tipo e restrições, consulte [lista de tipos](../statements/type-list.md).

Para criar um procedimento de construtor para uma classe, defina o nome de um `Sub` procedimento para a `New` palavra-chave. Para obter mais informações, consulte [tempo de vida do objeto: como os objetos são criados e destruídos](../../programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md).

A `New` palavra-chave pode ser usada nesses contextos:

- [Instrução Dim](../statements/dim-statement.md)
- [Desse](../statements/of-clause.md)
- [Instrução Sub](../statements/sub-statement.md)

## <a name="see-also"></a>Consulte também

- <xref:System.OutOfMemoryException>
- [Palavras-chave](../keywords/index.md)
- [Lista de Tipos](../statements/type-list.md)
- [Tipos genéricos no Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [Tempo de vida do objeto: como os objetos são criados e destruídos](../../programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)
