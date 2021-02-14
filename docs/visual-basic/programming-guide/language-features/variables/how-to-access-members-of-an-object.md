---
description: 'Saiba mais sobre: como acessar membros de um objeto (Visual Basic)'
title: Como acessar membros de um objeto
ms.date: 07/20/2015
helpviewer_keywords:
- members [Visual Basic], accessing
- object variables [Visual Basic], accessing members
ms.assetid: a0072514-6a79-4dd6-8d03-ca8c13e61ddc
ms.openlocfilehash: b4aed213bbe520b7b7027acc146d0973f7273fd1
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100435519"
---
# <a name="how-to-access-members-of-an-object-visual-basic"></a>Como acessar membros de um objeto (Visual Basic)

Quando você tem uma variável de objeto que se refere a um objeto, geralmente deseja trabalhar com os membros desse objeto, como seus métodos, propriedades, campos e eventos. Por exemplo, depois de criar um novo <xref:System.Windows.Forms.Form> objeto, talvez você queira definir sua <xref:System.Windows.Forms.Control.Text%2A> propriedade ou chamar seu <xref:System.Windows.Forms.Control.Focus%2A> método.

## <a name="accessing-members"></a>Acessando membros

Você acessa os membros de um objeto por meio da variável que faz referência a ele.

#### <a name="to-access-members-of-an-object"></a>Para acessar membros de um objeto

- Use o operador de acesso para membro ( `.` ) entre o nome da variável de objeto e o nome do membro.

    ```vb
    currentText = newForm.Text
    ```

    Se o membro for [compartilhado](../../../language-reference/modifiers/shared.md), você não precisará de uma variável para acessá-lo.

## <a name="accessing-members-of-an-object-of-known-type"></a>Acessando membros de um objeto de tipo conhecido

Se você souber o tipo de um objeto em tempo de compilação, poderá usar a *associação inicial* para uma variável que se refere a ele.

#### <a name="to-access-members-of-an-object-for-which-you-know-the-type-at-compile-time"></a>Para acessar membros de um objeto para o qual você sabe o tipo em tempo de compilação

1. Declare a variável de objeto para ser do tipo do objeto que você pretende atribuir à variável.

    ```vb
    Dim extraForm As System.Windows.Forms.Form
    ```

    Com o `Option Strict On` , você pode atribuir apenas <xref:System.Windows.Forms.Form> objetos (ou objetos de um tipo derivado de <xref:System.Windows.Forms.Form> ) para `extraForm` . Se você tiver definido uma classe ou estrutura com uma conversão de ampliação `CType` para <xref:System.Windows.Forms.Form> , também poderá atribuir essa classe ou estrutura a `extraForm` .

2. Use o operador de acesso para membro ( `.` ) entre o nome da variável de objeto e o nome do membro.

    ```vb
    extraForm.Show()
    ```

    Você pode acessar todos os métodos e propriedades específicos da <xref:System.Windows.Forms.Form> classe, independentemente da `Option Strict` configuração.

## <a name="accessing-members-of-an-object-of-unknown-type"></a>Acessando membros de um objeto de tipo desconhecido

Se você não souber o tipo de um objeto no momento da compilação, deverá usar a *ligação tardia* para qualquer variável que se refira a ele.

#### <a name="to-access-members-of-an-object-for-which-you-do-not-know-the-type-at-compile-time"></a>Para acessar membros de um objeto para o qual você não conhece o tipo em tempo de compilação

1. Declare a variável de objeto para ser do [tipo de dados Object](../../../language-reference/data-types/object-data-type.md). (Declarar uma variável como `Object` é o mesmo que declará-la como <xref:System.Object?displayProperty=nameWithType> .)

    ```vb
    Dim someControl As Object
    ```

    Com `Option Strict On` o, você pode acessar somente os membros que são definidos na <xref:System.Object> classe.

2. Use o operador de acesso para membro ( `.` ) entre o nome da variável de objeto e o nome do membro.

    ```vb
    someControl.GetType()
    ```

    Para poder acessar os membros de qualquer objeto que você atribui à variável de objeto, você deve definir `Option Strict Off` . Quando você faz isso, o compilador não pode garantir que um determinado membro seja exposto pelo objeto que você atribui à variável. Se o objeto não expõe um membro que você tenta acessar, ocorre uma <xref:System.MemberAccessException> exceção.

## <a name="see-also"></a>Consulte também

- <xref:System.Object>
- <xref:System.Windows.Forms.Form>
- <xref:System.MemberAccessException>
- [Variáveis de Objeto](object-variables.md)
- [Declaração de Variável do Objeto](object-variable-declaration.md)
- [Tipo de dados Object](../../../language-reference/data-types/object-data-type.md)
- [Instrução Option Strict](../../../language-reference/statements/option-strict-statement.md)
