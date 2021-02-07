---
description: 'Saiba mais sobre: como iniciar um aplicativo e enviar pressionamentos de tecla (Visual Basic)'
title: 'Como: iniciar um aplicativo e enviá-lo com pressionamentos de tecla-Visual Basic'
ms.date: 10/23/2019
helpviewer_keywords:
- keystrokes, sending
- Shell command example [Visual Basic]
- processes, starting and sending keystrokes
- SendKeys.SendWait examples
ms.assetid: f1303184-fce4-44fb-88b4-aac5f42d5d77
ms.openlocfilehash: ea54b940b528e0833d9c7a6cbef67f65a4cb4f6b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99666453"
---
# <a name="how-to-start-an-application-and-send-it-keystrokes-visual-basic"></a>Como: iniciar um aplicativo e enviar pressionamentos de tecla (Visual Basic)

Este exemplo usa o <xref:Microsoft.VisualBasic.Interaction.Shell%2A> método para iniciar o aplicativo do bloco de notas e, em seguida, imprime uma frase, enviando pressionamentos de teclas usando o método [My. Computer. Keyboard. SendKeys](xref:Microsoft.VisualBasic.Devices.Keyboard.SendKeys%2A) .

## <a name="example"></a>Exemplo

[!code-vb[VbVbalrMyComputer#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#25)]

## <a name="robust-programming"></a>Programação robusta

Uma <xref:System.ArgumentException> exceção será gerada se um aplicativo com o identificador de processo solicitado não puder ser encontrado.  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework

A chamada para a função `Shell` exige confiança total (classe <xref:System.Security.SecurityException>).

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.Devices.Keyboard.SendKeys%2A>
- <xref:Microsoft.VisualBasic.Interaction.Shell%2A>
- <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>
