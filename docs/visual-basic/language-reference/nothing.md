---
description: 'Saiba mais sobre: palavra-chave Nothing (Visual Basic)'
title: palavra-chave Nothing
ms.date: 07/20/2015
f1_keywords:
- Nothing
- vb.Nothing
helpviewer_keywords:
- Nothing keyword [Visual Basic]
- Nothing keyword [Visual Basic], syntax
ms.assetid: 06176e2d-bbf7-4a37-afaa-a86ad21ee99f
ms.openlocfilehash: c77f39c0a431dd05aabd24a235fb2dc88ea29e69
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99674721"
---
# <a name="nothing-keyword-visual-basic"></a>Palavra-chave Nothing (Visual Basic)

Representa o valor padrão de qualquer tipo de dados. Para tipos de referência, o valor padrão é a `null` referência. Para tipos de valor, o valor padrão depende se o tipo de valor é anulável.

> [!NOTE]
> Para tipos de valores não anuláveis, `Nothing` em Visual Basic difere de `null` em C#. Em Visual Basic, se você definir uma variável de um tipo de valor não anulável como `Nothing` , a variável será definida como o valor padrão para seu tipo declarado. No C#, se você atribuir uma variável de um tipo de valor não anulável a `null` , ocorrerá um erro em tempo de compilação.

## <a name="remarks"></a>Comentários

`Nothing` representa o valor padrão de um tipo de dados. O valor padrão depende se a variável é de um tipo de valor ou de um tipo de referência.

Uma variável de um *tipo Value* contém diretamente seu valor. Os tipos de valor incluem todos os tipos de dados numéricos,,,, `Boolean` `Char` `Date` todas as estruturas e todas as enumerações. Uma variável de um *tipo de referência* armazena uma referência a uma instância do objeto na memória. Os tipos de referência incluem classes, matrizes, delegados e cadeias de caracteres. Para obter mais informações, consulte [tipos de valor e tipos de referência](../programming-guide/language-features/data-types/value-types-and-reference-types.md).

Se uma variável for de um tipo Value, o comportamento de `Nothing` dependerá se a variável é de um tipo de dados anulável. Para representar um tipo de valor anulável, adicione um `?` modificador ao nome do tipo. A atribuição `Nothing` a uma variável anulável define o valor como `null` . Para obter mais informações e exemplos, consulte [tipos de valor anulável](../programming-guide/language-features/data-types/nullable-value-types.md).

Se uma variável for de um tipo de valor que não permite valor nulo, `Nothing` a atribuição a ela a definirá como o valor padrão para seu tipo declarado. Se esse tipo contiver Membros variáveis, todos eles serão definidos como seus valores padrão. O exemplo a seguir ilustra isso para tipos escalares.

[!code-vb[VbVbalrKeywords#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class2.vb#7)]

Se uma variável for de um tipo de referência, a atribuição `Nothing` à variável a definirá como uma `null` referência do tipo da variável. Uma variável que é definida como uma `null` referência não está associada a nenhum objeto. O exemplo a seguir demonstra este:

[!code-vb[VbVbalrKeywords#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/class3.vb#8)]

Ao verificar se uma variável de referência (ou tipo de valor anulável) é `null` , não use `= Nothing` ou `<> Nothing` . Sempre use `Is Nothing` ou `IsNot Nothing` .

Para cadeias de caracteres em Visual Basic, a cadeia vazia é igual a `Nothing` . Portanto, `"" = Nothing` é verdadeiro.

O exemplo a seguir mostra as comparações que usam os `Is` `IsNot` operadores e:

[!code-vb[VbVbalrKeywords#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class4.vb#9)]

Se você declarar uma variável sem usar uma `As` cláusula e defini-la como `Nothing` , a variável terá um tipo de `Object` . Um exemplo disso é `Dim something = Nothing` . Um erro de tempo de compilação ocorre nesse caso quando o `Option Strict` está ativado e `Option Infer` é desativado.

Quando você atribui `Nothing` a uma variável de objeto, ele não faz mais referência a nenhuma instância de objeto. Se a variável tiver referido anteriormente uma instância, defini-la como não `Nothing` terminará a instância em si. A instância é encerrada e os recursos de memória e sistema associados a ela são liberados, somente após o GC (coletor de lixo) detectar que não há nenhuma referência ativa restante.

`Nothing` difere do <xref:System.DBNull> objeto, que representa uma variante não inicializada ou uma coluna de banco de dados inexistente.

## <a name="see-also"></a>Consulte também

- [Instrução Dim](./statements/dim-statement.md)
- [Tempo de vida do objeto: como os objetos são criados e destruídos](../programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)
- [Tempo de vida no Visual Basic](../programming-guide/language-features/declared-elements/lifetime.md)
- [Operador Is](./operators/is-operator.md)
- [Operador IsNot](./operators/isnot-operator.md)
- [Tipos de valor anulável](../programming-guide/language-features/data-types/nullable-value-types.md)
