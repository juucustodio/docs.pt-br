---
description: 'Saiba mais sobre: tocando sons (Visual Basic)'
title: Executando sons
ms.date: 07/20/2015
helpviewer_keywords:
- system sounds, playing
- system sounds
- playing sounds, Visual Basic
- sound loops
- My.Computer.Audio object, tasks
- sounds, playing
- sounds, background
- playing sounds
ms.assetid: f0d9e4ab-57c7-47b6-86d3-99ff07078040
ms.openlocfilehash: 247af8274108ca8374cf87e53aa2aaad8e5e736c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99641506"
---
# <a name="playing-sounds-visual-basic"></a>Executando sons (Visual Basic)

O objeto `My.Computer.Audio` fornece métodos para reproduzir sons.  
  
## <a name="playing-sounds"></a>Executando sons  

 A reprodução em segundo plano permite que o aplicativo execute outro código enquanto o som é reproduzido. O método `My.Computer.Audio.Play` permite que o aplicativo para reproduza apenas um som de tela de fundo de cada vez. Quando o aplicativo reproduz um novo som de tela de fundo, ele para de reproduzir o som de tela de fundo anterior. Você também pode reproduzir um som e aguardar sua conclusão.  
  
 No exemplo a seguir, o método `My.Computer.Audio.Play` toca um som. Quando `AudioPlayMode.WaitToComplete` for especificado, `My.Computer.Audio.Play` aguardará até que o som seja concluído antes de o código de chamada continuar. Ao usar este exemplo, você deve garantir que o nome do arquivo se refere a um arquivo de som .wav no seu computador  
  
 [!code-vb[VbVbalrMyComputer#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class1.vb#15)]  
  
 No exemplo a seguir, o método `My.Computer.Audio.Play` toca um som. Ao usar este exemplo, você deve garantir que os recursos do aplicativo incluem um arquivo de som .wav chamado Waterfall.  
  
 [!code-vb[VbVbalrMyComputer#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class1.vb#16)]  
  
## <a name="playing-looping-sounds"></a>Reproduzindo sons em loop  

 No exemplo a seguir, o método `My.Computer.Audio.Play` toca o som especificado na tela de fundo quando `PlayMode.BackgroundLoop` é especificado. Ao usar este exemplo, você deve garantir que o nome do arquivo se refere a um arquivo de som .wav no seu computador.  
  
 [!code-vb[VbVbalrMyComputer#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class1.vb#11)]  
  
 No exemplo a seguir, o método `My.Computer.Audio.Play` toca o som especificado na tela de fundo quando `PlayMode.BackgroundLoop` é especificado. Ao usar este exemplo, você deve garantir que os recursos do aplicativo incluem um arquivo de som .wav chamado Waterfall.  
  
 [!code-vb[VbVbalrMyComputer#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class1.vb#12)]  
  
 O exemplo de código anterior também está disponível como um snippet de código do IntelliSense. No seletor de snippet de código, ele está localizado em **Aplicativos do Windows Forms &gt; Sons**. Para obter mais informações, consulte [Snippets de Código](/visualstudio/ide/code-snippets).  
  
 Em geral, quando um aplicativo reproduz um som em loop, ele deve interromper o som eventualmente.  
  
## <a name="stopping-the-playing-of-sounds-in-the-background"></a>Parando a reprodução de sons na tela de fundo  

 Use o método `My.Computer.Audio.Stop` para parar o som do aplicativo em loop ou na tela de fundo sendo reproduzido no momento.  
  
 Em geral, quando um aplicativo reproduz um som em loop, ele deve interromper o som em algum momento.  
  
 O exemplo a seguir interrompe um som que está sendo reproduzido na tela de fundo.  
  
 [!code-vb[VbVbalrMyComputer#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class1.vb#18)]  
  
 O exemplo de código anterior também está disponível como um snippet de código do IntelliSense. No seletor de snippet de código, ele está localizado em **Aplicativos do Windows Forms &gt; Sons**. Para obter mais informações, consulte [Snippets de Código](/visualstudio/ide/code-snippets).  
  
## <a name="playing-system-sounds"></a>Reproduzindo sons do sistema  

 Use o método `My.Computer.Audio.PlaySystemSound` para reproduzir o som do sistema especificado.  
  
 O método `My.Computer.Audio.PlaySystemSound` utiliza como parâmetro um dos membros compartilhados da classe <xref:System.Media.SystemSound>. O som do sistema <xref:System.Media.SystemSounds.Asterisk%2A> geralmente indica erros.  
  
 O exemplo a seguir usa o método `My.Computer.Audio.PlaySystemSound` para reproduzir um som do sistema.  
  
 [!code-vb[VbVbalrMyComputer#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class1.vb#17)]  
  
## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.Devices.Audio>
- <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A>
- <xref:Microsoft.VisualBasic.Devices.Audio.PlaySystemSound%2A>
- <xref:Microsoft.VisualBasic.Devices.Audio.Stop%2A>
- <xref:Microsoft.VisualBasic.AudioPlayMode>
