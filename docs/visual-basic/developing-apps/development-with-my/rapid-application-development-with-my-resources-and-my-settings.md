---
description: 'Saiba mais sobre: desenvolvimento rápido de aplicativos com My. Resources e My. Settings (Visual Basic)'
title: Método RAD com My.Resources e My.Settings
ms.date: 07/20/2015
helpviewer_keywords:
- My.Settings object [Visual Basic], developing applications
- rapid application development (RAD), My.Resources
- rapid application development (RAD), My.Settings
- My.Resources object [Visual Basic], developing applications
ms.assetid: 68284ab1-b685-4814-a2a4-01ae40445ff8
ms.openlocfilehash: 38846b3a6ac273306f588ad8b043d7f35f7230a0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797920"
---
# <a name="rapid-application-development-with-myresources-and-mysettings-visual-basic"></a>Desenvolvimento de aplicativo rápido com My.Resources e My.Settings (Visual Basic)

O `My.Resources` objeto fornece acesso aos recursos do aplicativo e permite que você recupere dinamicamente os recursos para seu aplicativo.  
  
## <a name="retrieving-resources"></a>Recuperando recursos  

 Vários recursos, como arquivos de áudio, ícones, imagens e cadeias de caracteres, podem ser recuperados por meio do `My.Resources` objeto. Por exemplo, você pode acessar os arquivos de recursos específicos da cultura do aplicativo. O exemplo a seguir define o ícone do formulário para o ícone chamado `Form1Icon` armazenado no arquivo de recurso do aplicativo.  
  
 [!code-vb[VbVbcnMy#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#7)]  
  
 O `My.Resources` objeto expõe apenas recursos globais. Ele não fornece acesso aos arquivos de recursos associados aos formulários. Acesse os recursos do formulário no formulário.  
  
 Da mesma forma, o `My.Settings` objeto fornece acesso às configurações do aplicativo e permite que você armazene e recupere dinamicamente as configurações de propriedade e outras informações para seu aplicativo. Para obter mais informações, consulte [My. Resources](../../language-reference/objects/my-resources-object.md) Object e [My. Settings Object](../../language-reference/objects/my-settings-object.md).  
  
## <a name="see-also"></a>Consulte também

- [Objeto My.Resources](../../language-reference/objects/my-resources-object.md)
- [Objeto My.Settings](../../language-reference/objects/my-settings-object.md)
- [Acessando configurações de aplicativo](../programming/app-settings/index.md)
