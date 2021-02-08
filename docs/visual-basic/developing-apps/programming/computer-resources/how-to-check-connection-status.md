---
description: 'Saiba mais sobre: como verificar o status da conexão no Visual Basic'
title: 'Como: Verificar o status da conexão'
ms.date: 07/20/2015
helpviewer_keywords:
- Web connections [Visual Basic]
- IsAvailable property [Visual Basic], about IsAvailable
- connections [Visual Basic], checking status
- connection status [Visual Basic]
ms.assetid: 4d9ee8ab-9a6f-4279-ace4-b75afc976a74
ms.openlocfilehash: c568e3be5d8fedb1ae12c748110b23218deaf069
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797738"
---
# <a name="how-to-check-connection-status-in-visual-basic"></a>Como verificar o status da conexão no Visual Basic

A propriedade <xref:Microsoft.VisualBasic.Devices.Network.IsAvailable> pode ser usada para determinar se o computador tem uma rede ou conexão de Internet em funcionamento.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-check-whether-a-computer-has-a-working-connection"></a>Para verificar se um computador tem uma conexão em funcionamento  
  
- Determine se a propriedade `IsAvailable` é `True` ou `False`. O código a seguir verifica e informa o status da propriedade:  
  
     [!code-vb[VbResourceTasks#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#3)]  
  
     Este exemplo de código também está disponível como um snippet de código do IntelliSense. No selecionador de snippet de código, ele está localizado em **Conectividade e Redes**. Para obter mais informações, consulte [Snippets de Código](/visualstudio/ide/code-snippets).  
  
## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.Devices.Network?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Devices.Network.IsAvailable>
