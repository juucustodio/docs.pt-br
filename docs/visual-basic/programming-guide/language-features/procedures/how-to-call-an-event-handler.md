---
title: Como chamar um manipulador de eventos
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- event handlers [Visual Basic], calling
- event handlers
- procedures [Visual Basic], event handlers
- procedures [Visual Basic], calling
no-loc:
- WithEvents
ms.assetid: 72e18ef8-144e-40df-a1f4-066a57271e28
ms.openlocfilehash: 3762c79dd3d883ae2ccfe76b335cf98ac87d4246
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89464955"
---
# <a name="how-to-call-an-event-handler-in-visual-basic"></a>Como chamar um manipulador de eventos no Visual Basic

Um *evento* é uma ação ou ocorrência — como um clique do mouse ou um limite de crédito excedido — que é reconhecido por algum componente do programa e para o qual você pode escrever código para responder. Um *manipulador de eventos* é o código que você escreve para responder a um evento.

Um manipulador de eventos no Visual Basic é um `Sub` procedimento. No entanto, você normalmente não o chama da mesma maneira que outros `Sub` procedimentos. Em vez disso, você identifica o procedimento como um manipulador para o evento. Isso pode ser feito com uma [`Handles`](../../../language-reference/statements/handles-clause.md) cláusula e uma [`WithEvents`](../../../language-reference/modifiers/withevents.md) variável, ou com uma [instrução AddHandler](../../../language-reference/statements/addhandler-statement.md). O uso de uma `Handles` cláusula é a maneira padrão de declarar um manipulador de eventos em Visual Basic. Essa é a maneira como os manipuladores de eventos são escritos pelos designers quando você programa no ambiente de desenvolvimento integrado (IDE). A `AddHandler` instrução é adequada para gerar eventos dinamicamente em tempo de execução.

Quando o evento ocorre, Visual Basic chama automaticamente o procedimento do manipulador de eventos. Qualquer código que tenha acesso ao evento pode fazer com que ele ocorra executando uma [instrução RaiseEvent](../../../language-reference/statements/raiseevent-statement.md).

Você pode associar mais de um manipulador de eventos com o mesmo evento. Em alguns casos, você pode dissociar um manipulador de um evento. Para obter mais informações, consulte [Eventos](../events/index.md).

## <a name="call-an-event-handler-using-no-loc-texthandles-and-no-locwithevents"></a>Chamar um manipulador de eventos usando :::no-loc text="Handles"::: e WithEvents

1. Verifique se o evento é declarado com uma [instrução de evento](../../../language-reference/statements/event-statement.md).

2. Declare uma variável de objeto no nível de módulo ou classe, usando a [`WithEvents`](../../../language-reference/modifiers/withevents.md) palavra-chave. A `As` cláusula para essa variável deve especificar a classe que gera o evento.

3. Na declaração do procedimento de manipulação de eventos `Sub` , adicione uma [`Handles`](../../../language-reference/statements/handles-clause.md) cláusula que especifica a `WithEvents` variável e o nome do evento.

4. Quando o evento ocorre, Visual Basic chama automaticamente o `Sub` procedimento. Seu código pode usar uma `RaiseEvent` instrução para fazer o evento ocorrer.

    O exemplo a seguir define um evento e uma `WithEvents` variável que se refere à classe que gera o evento. O procedimento de manipulação de eventos `Sub` usa uma `Handles` cláusula para especificar a classe e o evento que ele manipula.

    :::code language="vb" source="snippets/how-to-call-an-event-handler/SpecialForm.vb" id="4":::

## <a name="call-an-event-handler-using-addhandler"></a>Chamar um manipulador de eventos usando AddHandler

1. Verifique se o evento é declarado com uma `Event` instrução.

2. Execute uma [instrução AddHandler](../../../language-reference/statements/addhandler-statement.md) para conectar dinamicamente o procedimento de manipulação de eventos `Sub` com o evento.

3. Quando o evento ocorre, Visual Basic chama automaticamente o `Sub` procedimento. Seu código pode usar uma `RaiseEvent` instrução para fazer o evento ocorrer.

    O exemplo a seguir usa a [instrução AddHandler](../../../language-reference/statements/addhandler-statement.md) no construtor para associar o `OnFormClosing` procedimento como um manipulador de eventos para <xref:System.Windows.Forms.Form.FormClosing> .

    :::code language="vb" source="snippets/how-to-call-an-event-handler/SpecialForm.vb" id="5":::

    Você pode dissociar um manipulador de eventos de um evento executando a [instrução RemoveHandler](../../../language-reference/statements/removehandler-statement.md).

## <a name="see-also"></a>Veja também

- [Procedimentos](index.md)
- [Subprocedimentos](sub-procedures.md)
- [Instrução Sub](../../../language-reference/statements/sub-statement.md)
- [Operador AddressOf](../../../language-reference/operators/addressof-operator.md)
- [Como criar um procedimento](how-to-create-a-procedure.md)
- [Como chamar um procedimento que não retorne um valor](how-to-call-a-procedure-that-does-not-return-a-value.md)
