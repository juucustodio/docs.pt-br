---
description: 'Saiba mais sobre: como: usar componentes que dão suporte ao padrão assíncrono baseado em evento'
title: 'Como: Usar componentes compatíveis com o padrão assíncrono baseado em evento'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET], asynchronous features
- components [.NET], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 35e9549c-1568-4768-ad07-17cc6dff11e1
ms.openlocfilehash: 78c5df143e687333689e7805dfc89b4cf0f5e98a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99702958"
---
# <a name="how-to-use-components-that-support-the-event-based-asynchronous-pattern"></a>Como: Usar componentes compatíveis com o padrão assíncrono baseado em evento

Muitos componentes oferecem a opção de executar seu trabalho de forma assíncrona. Os componentes <xref:System.Media.SoundPlayer> e <xref:System.Windows.Forms.PictureBox>, por exemplo, permite que você carregue sons e imagens "em segundo plano", enquanto o thread principal continua em execução sem interrupções.  
  
 Usar métodos assíncronos em uma classe que dá suporte à [Visão geral do padrão assíncrono baseado em evento](event-based-asynchronous-pattern-overview.md) pode ser tão simples quanto anexar um manipulador de eventos ao evento _MethodName_**Completed** do componente, assim como você faria com qualquer outro evento. Quando você chama o método _MethodName_**Async**, seu aplicativo continuará sendo executado sem interrupção até que o evento _MethodName_**Completed** seja gerado. No manipulador de eventos, você pode examinar o parâmetro <xref:System.ComponentModel.AsyncCompletedEventArgs> para determinar se a operação assíncrona foi concluída com êxito ou se foi cancelada.  
  
 Para saber mais sobre como usar manipuladores de evento, consulte [Visão geral dos manipuladores de evento](/dotnet/desktop/winforms/event-handlers-overview-windows-forms).  
  
 O procedimento a seguir mostra como usar o recurso de carregamento de imagem assíncrono de um controle <xref:System.Windows.Forms.PictureBox>.  
  
### <a name="to-enable-a-picturebox-control-to-asynchronously-load-an-image"></a>Para ativar um controle PictureBox para carregar assincronamente uma imagem  
  
1. Crie uma instância do componente <xref:System.Windows.Forms.PictureBox> no formulário.  
  
2. Atribua um manipulador de eventos ao evento <xref:System.Windows.Forms.PictureBox.LoadCompleted>.  
  
     Verifique se ocorreu algum erro durante o download assíncrono aqui. Verifique também o cancelamento.  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#2](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#2](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#2)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#5)]  
  
3. Adicione dois botões, chamados `loadButton` e `cancelLoadButton`, ao formulário. Adicione <xref:System.Windows.Forms.Control.Click> manipuladores de eventos para iniciar e cancelar o download.  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#4)]  
  
4. Execute seu aplicativo.  
  
     Conforme o download da imagem prossegue, você pode mover o formulário livremente, minimizá-lo e maximizá-lo.  
  
## <a name="see-also"></a>Consulte também

- [Como: Executar uma operação em segundo plano](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)
- [Visão geral do padrão assíncrono baseado em evento](event-based-asynchronous-pattern-overview.md)
