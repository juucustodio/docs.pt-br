---
description: 'Saiba mais sobre: como chamar um procedimento que não retorna um valor (Visual Basic)'
title: Como chamar um procedimento que não retorne um valor
ms.date: 07/20/2015
helpviewer_keywords:
- procedure calls [Visual Basic], returning values
- Visual Basic code, procedures
- procedures [Visual Basic], calling
ms.assetid: 259b49a3-a3c1-4254-ba8c-73cdc4127703
ms.openlocfilehash: 3aaa6b4358f0585323e6c8321eea7dbaa4906a44
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100466764"
---
# <a name="how-to-call-a-procedure-that-does-not-return-a-value-visual-basic"></a>Como chamar um procedimento que não retorne um valor (Visual Basic)

Um `Sub` procedimento não retorna um valor para o código de chamada. Você o chama explicitamente com uma instrução de chamada autônoma. Você não pode chamá-lo simplesmente usando seu nome dentro de uma expressão.  
  
### <a name="to-call-a-sub-procedure"></a>Para chamar um procedimento Sub  
  
1. Especifique o nome do `Sub` procedimento.  
  
2. Siga o nome do procedimento com parênteses para colocar a lista de argumentos. Se não houver argumentos, você pode opcionalmente omitir os parênteses. No entanto, usar os parênteses torna seu código mais fácil de ler.  
  
3. Coloque os argumentos na lista de argumentos dentro dos parênteses, separados por vírgulas. Certifique-se de fornecer os argumentos na mesma ordem em que o `Sub` procedimento define os parâmetros correspondentes.  
  
     O exemplo a seguir chama a <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> função Visual Basic para ativar uma janela de aplicativo. <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> usa o título da janela como seu único argumento. Ele não retorna um valor para o código de chamada. Se um processo do bloco de notas não estiver em execução, o exemplo lançará um <xref:System.ArgumentException> . O `Shell` procedimento pressupõe que os aplicativos estão nos caminhos especificados.  
  
     [!code-vb[VbVbalrCatRef#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCatRef/VB/Class1.vb#11)]  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Interaction.Shell%2A>
- <xref:System.ArgumentException>
- [Procedimentos](./index.md)
- [Subprocedimentos](./sub-procedures.md)
- [Parâmetros e Argumentos de Procedimento](./procedure-parameters-and-arguments.md)
- [Instrução Sub](../../../language-reference/statements/sub-statement.md)
- [Como criar um procedimento](./how-to-create-a-procedure.md)
- [Como chamar um procedimento que retorna um valor](./how-to-call-a-procedure-that-returns-a-value.md)
- [Como chamar um manipulador de eventos no Visual Basic](./how-to-call-an-event-handler.md)
